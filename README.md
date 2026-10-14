use code to commiit changes 
commit changes by using the code 89
import urllib.request
import json

def fetch_github_profile(username):
    """Fetches public information about a GitHub user."""
    url = f"https://github.com{username}"
    
    # Custom User-Agent header required by the GitHub API
    req = urllib.request.Request(url, headers={'User-Agent': 'GitHub-Profile-Analyzer'})
    
    try:
        with urllib.request.urlopen(req) as response:
            if response.status == 200:
                data = json.loads(response.read().decode())
                
                print(f"\n--- GitHub Profile: {data.get('login')} ---")
                print(f"Name: {data.get('name', 'N/A')}")
                print(f"Bio: {data.get('bio', 'No bio available')}")
                print(f"Public Repos: {data.get('public_repos')}")
                print(f"Followers: {data.get('followers')}")
                print(f"Following: {data.get('following')}")
                print(f"Profile URL: {data.get('html_url')}")
                print("-" * 30)
            else:
                print(f"Error: Received status code {response.status}")
    except Exception as e:
        print(f"Could not fetch profile. Error: {e}")

if __name__ == "__main__":
    # You can change 'octocat' to any real GitHub username to test it
    user_to_check = input("Enter a GitHub username to analyze (e.g., octocat): ").strip()
    fetch_github_profile(user_to_check)
