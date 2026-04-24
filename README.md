# SelbySpace MCP Server

An MCP (Model Context Protocol) server that integrates with your SelbySpace GitHub repository, enabling seamless interaction with your repo through ChatGPT and other compatible AI interfaces.

## Features

- **Repository Information**: Get details about your SelbySpace repository
- **Issue Management**: List and query repository issues
- **Pull Request Access**: Browse pull requests and their metadata
- **File Operations**: Read files and explore directory structures
- **Commit History**: Retrieve and analyze recent commits

## Setup Instructions

### 1. Clone or Download This Repository

```bash
git clone https://github.com/nickselby-KW/SelbySpace.git
cd SelbySpace
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

Edit `.env` and add:

```
GITHUB_TOKEN=your_github_personal_access_token_here
GITHUB_OWNER=nickselby-KW
GITHUB_REPO=SelbySpace
MCP_PORT=3000
```

**To get your GitHub token:**
1. Go to https://github.com/settings/tokens
2. Click "Generate new token" (classic or fine-grained)
3. Select scopes: `repo`, `read:user`
4. Copy and paste into `.env`

### 4. Build the Server

```bash
npm run build
```

### 5. Deploy to Production

#### Option A: Deploy on Vercel (Recommended - Free & Easy)

1. Push your code to GitHub
2. Go to https://vercel.com/new
3. Select your SelbySpace repository
4. Add environment variables in Vercel dashboard:
   - `GITHUB_TOKEN`
   - `GITHUB_OWNER`
   - `GITHUB_REPO`
5. Deploy

Your MCP server will be available at: `https://[your-vercel-project].vercel.app`

#### Option B: Deploy on Railway (Alternative)

1. Go to https://railway.app
2. Create new project → GitHub repo
3. Add environment variables
4. Deploy

Your MCP server will be available at: `https://[railway-domain]`

#### Option C: Deploy on Heroku

1. Install Heroku CLI
2. Run:
```bash
heroku create your-selbytime-mcp
git push heroku main
heroku config:set GITHUB_TOKEN=your_token
```

Your MCP server will be available at: `https://your-selbytime-mcp.herokuapp.com`

### 6. Connect to ChatGPT

Once deployed, add this MCP server to ChatGPT:

1. In ChatGPT settings → Integrations
2. Add MCP Server
3. Enter your public URL: `https://[your-deployment-url]`
4. Set authentication headers if required

## Local Testing

To test locally:

```bash
npm run dev
```

This starts the MCP server on stdio transport.

## Available Tools

- **get_repo_info**: Retrieve repository metadata
- **list_issues**: Get issues (filter by open/closed/all)
- **list_pull_requests**: Get pull requests (filter by open/closed/all)
- **get_file**: Read file contents from the repository
- **list_files**: Browse directory contents
- **get_commits**: Get recent commit history

## Troubleshooting

**"GITHUB_TOKEN environment variable is required"**
- Add your token to `.env` file

**"Not Found" errors when accessing files**
- Verify file paths are correct
- Ensure token has proper permissions

**MCP Server not connecting**
- Check that your deployment URL is publicly accessible
- Verify all environment variables are set

## Architecture

This MCP server uses:
- **@modelcontextprotocol/sdk**: MCP protocol implementation
- **octokit**: GitHub API client
- **TypeScript**: Type-safe implementation
- **Node.js**: Runtime environment

## License

MIT