Website Snapshot Automator
Overview
This Python script is a powerful tool designed to assist UX/UI teams by automating the process of capturing screenshots for entire websites. When starting a new project, redesign, or audit, it's often necessary to capture the current state of a website across different devices. This script streamlines that workflow, saving hours of manual work.

It crawls a given website, discovers all accessible pages within the same domain, and takes full-page screenshots at pre-defined mobile, tablet, and desktop viewport sizes.

✨ For the UX Team
This tool was built to facilitate and accelerate the initial phases of our design and audit processes. Instead of manually visiting and capturing each page, you can run this single script to get a complete visual inventory of a website, ensuring consistent and comprehensive captures for analysis, presentations, and archival purposes.

We also have a Figma plugin version of this tool, which integrates directly into your design workflow!

Key Features
Automated Website Crawling: Starts from a single URL and recursively finds all internal links on the domain.

Multi-Device Simulation: Captures screenshots in three standard portrait sizes:

Mobile (375x667)

Tablet (768x1024)

Desktop (1440x900)

Full-Page Capture: Scrolls and captures the entire length of each page, not just the visible portion.

Organized Output: Saves all screenshots into a designated folder, with clear, descriptive filenames indicating the page and device type.

Error Handling: Includes retries for network requests and gracefully handles errors during the screenshot process.

How to Use
1. Prerequisites
Python 3.x installed on your system.

pip (Python's package installer).

2. Setup & Installation
Clone the repository (or download the script):

git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

Install the required Python libraries:
This script uses Playwright to control a headless browser. The first command installs the necessary Python packages, and the second command downloads the required browser binaries.

pip install playwright beautifulsoup4 requests nest-asyncio
playwright install

3. Configuration
Before running the script, you need to set two main variables inside the main() function at the bottom of the script:

start_website_url: The initial URL where the crawler will begin.

output_dir: The name of the folder where the screenshots will be saved.

async def main():
    # --- CONFIGURE THESE VALUES ---
    start_website_url = "https://www.world-kinect.com/blog"
    output_dir = "blog_snapshots"
    # ----------------------------

    all_website_links = crawl_website(start_website_url)

    for link in all_website_links:
        await take_screenshot(link, "mobile", output_folder=output_dir)
        await take_screenshot(link, "tablet", output_folder=output_dir)
        await take_screenshot(link, "desktop", output_folder=output_dir)

    print(f"Screenshots saved to '{output_dir}' directory.")

4. Running the Script
Once configured, execute the script from your terminal:

python your_script_name.py

The script will print its progress as it crawls the site and saves the screenshots. When finished, you will find a new directory (e.g., blog_snapshots) filled with the captured images.

Customization
You can easily customize the device viewports by modifying the device_settings dictionary within the take_screenshot function. This allows you to add new devices or change the dimensions to match specific project requirements.

def take_screenshot(url, device_type, output_folder="screenshots"):
    """Takes a screenshot of a URL in specified device emulation."""
    device_settings = {
        "mobile": {"viewport": {"width": 375, "height": 667}, ...},
        "tablet": {"viewport": {"width": 768, "height": 1024}, ...},
        "desktop": {"viewport": {"width": 1440, "height": 900}, ...},
        # You can add a new device here!
        "small-mobile": {"viewport": {"width": 320, "height": 568}, ...}
    }
    ...

Dependencies
Playwright: For browser automation and capturing screenshots.

Beautiful Soup: For parsing HTML and extracting links.

Requests: For making HTTP requests to fetch web pages.

nest-asyncio: To manage the asynchronous event loop within a Jupyter/IPython environment.

License
This project is licensed under the MIT License. See the LICENSE.md file for details.
