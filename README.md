# Step 1: Import necessary libraries
import requests
import time
from PIL import Image
from IPython.display import display, HTML
from io import BytesIO

# Step 2: Set up API keys
DEEPAI_API_KEY = "your-deepai-api-key-here"  # Replace with real DeepAI key
HF_TOKEN = "your-huggingface-token-here"    # Replace with real Hugging Face token

# Step 3: Define the prompt template for image and text
prompt_template = """
Create a social media post for a recipe generating website, promoting a specific dish.
Product name: {product_name}
Required dish: {dish}
Key message: {key_message}
Written tone: {tone} (e.g., craft the caption to feel calm, exciting, or friendly)
Image color scheme: {color_scheme} (use this as the dominant palette in the image)

Output:
1. A short, engaging social media caption (50-100 words) that promotes the {dish} recipe, aligns with the {tone} tone, and incorporates the {key_message}.
2. A detailed image prompt for AI image generators, describing a photorealistic, high-detail 1024x1024 image featuring the {dish} in a {tone} atmosphere, using a {color_scheme} color palette, with the {key_message} subtly integrated (e.g., text overlay or thematic elements).
"""

# Step 4: Function to collect client inputs with defaults
def collect_client_inputs():
    product_name = input("Enter the product name (e.g., RecipeGenius) [default: RecipeGenius]: ") or "RecipeGenius"
    dish = input("Enter the required dish (e.g., Spaghetti Carbonara) [default: Spaghetti Carbonara]: ") or "Spaghetti Carbonara"
    key_message = input("Enter the key message (e.g., Cook with ease!) [default: Cook with ease!]: ") or "Cook with ease!"
    tone = input("Enter the written tone (e.g., calm, exciting, friendly) [default: friendly]: ") or "friendly"
    color_scheme = input("Enter the image color scheme (e.g., warm reds, cool blues) [default: warm reds]: ") or "warm reds"
    return product_name, dish, key_message, tone, color_scheme

# Step 5: Function to generate the prompt and simulate LLM output
def generate_recipe_content(product_name, dish, key_message, tone, color_scheme):
    # Fill the prompt template
    recipe_prompt = prompt_template.format(
        product_name=product_name,
        dish=dish,
        key_message=key_message,
        tone=tone,
        color_scheme=color_scheme
    )
    # Simulate LLM response (in practice, send to an LLM API like Grok)
    caption = (
        f"Whip up a delicious {dish} with {product_name}! {key_message} "
        f"Follow our easy recipe to create a {tone} dining experience. "
        f"Discover more at {product_name.lower()}.com! #Recipes #{dish.replace(' ', '')}"
    )
    image_prompt = (
        f"A photorealistic 1024x1024 social media graphic featuring a beautifully plated {dish}, "
        f"set in a {tone} atmosphere, with a {color_scheme} color palette dominating the scene. "
        f"The {key_message} is subtly integrated via elegant text overlay or thematic elements, "
        f"surrounded by fresh ingredients and a modern kitchen setting, high detail, vibrant lighting."
    )
    return recipe_prompt, caption, image_prompt

# Step 6: Function to display an image in Colab
def display_image(source, source_type="url"):
    try:
        if source_type == "url":
            response = requests.get(source)
            response.raise_for_status()
            img = Image.open(BytesIO(response.content))
        else:  # local
            img = Image.open(source)
        
        img = img.resize((512, 512))  # Resize for notebook
        print(f"Displaying image from {source_type}: {source}")
        display(img)
    except Exception as e:
        print(f"Error displaying image: {str(e)}")

# Step 7: Function to generate image using DeepAI
def get_deepai_image(image_prompt):
    try:
        url = "https://api.deepai.org/api/text2img"
        data = {'text': image_prompt}
        headers = {'api-key': DEEPAI_API_KEY}
        response = requests.post(url, data=data, headers=headers)
        response.raise_for_status()
        result = response.json()
        if 'id' in result:
            poll_url = f"https://api.deepai.org/api/job/{result['id']}"
            while True:
                poll_response = requests.get(poll_url, headers=headers)
                poll_result = poll_response.json()
                if poll_result.get('status') == 'success':
                    return poll_result['output_url']
                elif poll_result.get('status') == 'failed':
                    return f"Error: {poll_result.get('err', 'Unknown error')}"
                time.sleep(3)
        else:
            return f"Error: {result.get('err', 'No ID returned')}"
    except Exception as e:
        return f"Error generating DeepAI image: {str(e)}"

# Step 8: Function to generate image using Pollinations
def get_pollinations_image(image_prompt):
    try:
        gen_url = f"https://pollinations.ai/p/{image_prompt.replace(' ', '%20')}?width=1024&height=1024&seed=42"
        return gen_url
    except Exception as e:
        return f"Error generating Pollinations image: {str(e)}"

# Step 9: Function to generate image using Hugging Face
def get_huggingface_image(image_prompt):
    try:
        url = "https://api-inference.huggingface.co/models/stabilityai/stable-diffusion-2-1"
        headers = {"Authorization": f"Bearer {HF_TOKEN}"}
        payload = {"inputs": image_prompt}
        response = requests.post(url, headers=headers, json=payload)
        response.raise_for_status()
        if response.headers.get('content-type') == 'image/png':
            filename = 'hf_image.png'
            with open(filename, 'wb') as f:
                f.write(response.content)
            return filename
        else:
            result = response.json()
            return f"Error: {result.get('error', 'Unknown error')}"
    except Exception as e:
        return f"Error generating Hugging Face image: {str(e)}"

# Step 10: Function to present results (caption and images)
def present_results(caption, deepai_url, pollinations_url, hf_result):
    print("\n=== Social Media Caption ===")
    print(caption)
    
    print("\n=== DeepAI Image ===")
    if "Error" not in str(deepai_url):
        display_image(deepai_url, "url")
    else:
        print(deepai_url)
    
    print("\n=== Pollinations Image ===")
    if "Error" not in str(pollinations_url):
        display_image(pollinations_url, "url")
    else:
        print(pollinations_url)
    
    print("\n=== Hugging Face Image ===")
    if "Error" not in str(hf_result) and hf_result.endswith('.png'):
        display_image(hf_result, "local")
    else:
        print(hf_result)
    
    print("\nChoose your favorite image and caption combo!")

# Step 11: Main function
def main():
    # Collect inputs
    product_name, dish, key_message, tone, color_scheme = collect_client_inputs()
    
    # Generate content
    recipe_prompt, caption, image_prompt = generate_recipe_content(
        product_name, dish, key_message, tone, color_scheme
    )
    print("\nGenerated Recipe Prompt:")
    print(recipe_prompt)
    print("\nGenerated Image Prompt:")
    print(image_prompt)
    
    # Generate images
    print("\nGenerating DeepAI image...")
    deepai_url = get_deepai_image(image_prompt)
    
    print("Generating Pollinations image...")
    pollinations_url = get_pollinations_image(image_prompt)
    
    print("Generating Hugging Face image...")
    hf_result = get_huggingface_image(image_prompt)
    
    # Present results
    present_results(caption, deepai_url, pollinations_url, hf_result)

# Step 12: Run it!
if __name__ == "__main__":
    main()
