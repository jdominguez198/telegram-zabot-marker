# Telegram ZABot Marker

## Requirements

To start using this GitHub Action you should have first the following requirements:

1. Fork this repository into your GitHub profile
2. Create a private repository with a Telegram Session state files (`auth`, `secret`, `state`)
3. Add Repository Secrets in your repository Settings 

### Create Telegram Session

To create a Telegram Session state files you must follow the below steps:

- Open your favorite terminal and change to a clean directory
- Run the following Docker command: 
```bash
docker run -v "$(pwd)":/root/.telegram-cli weibeld/ubuntu-telegram-cli bin/telegram-cli
```
- Once you run it, the prompt will ask you for a working mobile phone to send a verification code. Then, use the
code received in the mobile phone to create the session
- Stop the Docker container, and you'll see the files in your current directory

Now, create a private repository with the files `auth`, `secret`, and `state` in the root directory

### Add Repository Secrets

Navigate to `Settings > Secrets > Actions` in your forked repository and create the following repository secrets
clicking on `New repository secret` button:

- `AUTH_REPOSITORY` => this should be your repository forked. Example: `my_github_profile/my_forked_repo`
- `REPO_TOKEN` => Personal Access Token with repo private privileges and workflows

## Usage

Once you have completed the requirements, you can use GitHub Actions to fire the workflow.

### Test Action

Use curl to make a request and trigger the workflow:

```bash
curl -X POST \
  -H "Authorization: token <YOUR_PERSONAL_ACCESS_TOKEN>" \
  -H "Accept: application/vnd.github.v3+json" \
  -d '{"event_type":"marker_test"}' \
  https://api.github.com/repos/<YOUR_USERNAME>/<YOUR_FORKED_REPOSITORY>/dispatches
```

### Real Action

Use curl to make a request and trigger the workflow:

```bash
curl -X POST \
  -H "Authorization: token <YOUR_PERSONAL_ACCESS_TOKEN>" \
  -H "Accept: application/vnd.github.v3+json" \
  -d '{"event_type":"marker"}' \
  https://api.github.com/repos/<YOUR_USERNAME>/<YOUR_FORKED_REPOSITORY>/dispatches
```
