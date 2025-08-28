# site_checker.py
import argparse
import requests

def check_website_status(url):
    """
    Checks the status of a given URL and prints the result.
    """
    try:
        # Add a timeout to prevent the script from hanging indefinitely
        response = requests.get(url, timeout=5)
        
        # Check if the status code is 200 (OK)
        if response.status_code == 200:
            print(f"Success! '{url}' is online and returned status code 200.")
        else:
            print(f"Warning: '{url}' is reachable but returned status code {response.status_code}.")
            
    except requests.exceptions.Timeout:
        print(f"Error: The request to '{url}' timed out.")
    except requests.exceptions.RequestException as e:
        print(f"Error: Could not connect to '{url}'. Reason: {e}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Check the status of a website.")
    parser.add_argument("url", help="The URL of the website to check.")
    
    args = parser.parse_args()
    check_website_status(args.url)
