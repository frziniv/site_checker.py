import argparse
import requests

# ANSI escape codes for colors
COLOR_GREEN = '\033[92m'
COLOR_YELLOW = '\033[93m'
COLOR_RED = '\033[91m'
COLOR_RESET = '\033[0m'

def check_website_status(url):
    """
    Checks the status of a given URL and prints a color-coded result.
    """
    try:
        # Add a timeout to prevent the script from hanging indefinitely
        response = requests.get(url, timeout=5)
        
        # Check if the status code is 200 (OK)
        if response.status_code == 200:
            print(f"{COLOR_GREEN}Success! '{url}' is online and returned status code 200.{COLOR_RESET}")
        else:
            print(f"{COLOR_YELLOW}Warning: '{url}' is reachable but returned status code {response.status_code}.{COLOR_RESET}")
            
    except requests.exceptions.Timeout:
        print(f"{COLOR_RED}Error: The request to '{url}' timed out.{COLOR_RESET}")
    except requests.exceptions.RequestException as e:
        print(f"{COLOR_RED}Error: Could not connect to '{url}'. Reason: {e}{COLOR_RESET}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Check the status of a website.")
    parser.add_argument("url", help="The URL of the website to check.")
    
    args = parser.parse_args()
    check_website_status(args.url)
