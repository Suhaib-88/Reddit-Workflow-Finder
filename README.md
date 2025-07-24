# Reddit n8n Workflow Setup Guide

<img width="1220" height="554" alt="image" src="https://github.com/user-attachments/assets/7a124506-f66d-4577-a685-f412710985c1" />

###  Workflow Description
This n8n workflow is a Reddit workflow Finder that automatically scrapes Reddit posts from specified subreddits, filters for posts containing valuable resources (GitHub repositories, YouTube videos, or Google Docs/Drive links), and stores the results in Airtable for easy organization and analysis.

### What It Does:
- Monitors Reddit: Automatically searches specific subreddits for posts containing certain keywords. 
- Filters Content: Only captures posts that include GitHub repos, YouTube videos, or Google Drive/Docs links
- Stores Results: Saves all data to Airtable with proper formatting

### Prerequisites
Required Accounts:
- n8n Instance (cloud or self-hosted)
- Apify Account (for Reddit scraping)
- Airtable Account (for data storage)

### API Tokens Needed:
- Apify API token
- Airtable Personal Access Token

## Step-by-Step Setup Instructions

### Step 1: Set Up Apify Account

1. **Create Apify Account**:
   - Go to [apify.com](https://apify.com)
   - Sign up for a free account

2. **Get API Token**:
   - Navigate to Settings → Integrations
   - Copy your API token
   - Keep this token secure - you'll need it in Step 4

3. **Verify Actor Availability**:
   - The workflow uses two actors:
     - https://apify.com/moving_beacon-owner1/my-actor-26

### Step 2: Set Up Airtable

1. **Create Airtable Account**:
   - Go to [airtable.com](https://airtable.com)
   - Sign up for a free account

2. **Create a New Base**:
   - Click "Create a base"
   - Name it "Reddit_posts" or similar

3. **Set Up Table Structure**:
   Create a table named "Reddit Open Source" with these fields:
   - `id` (Single line text) - Primary field
   - `Name` (Single line text) - Reddit username
   - `header` (Long text) - Post title
   - `body_text` (Long text) - Post content
   - `link` (URL) - Reddit post link
   - extracted_links- Opensource extracted links( github, youtube, drive, docs etc)

4. **Get Airtable Credentials**:
   - Go to [airtable.com/create/tokens](https://airtable.com/create/tokens)
   - Create a Personal Access Token
   - Give it access to your base with read/write permissions
   - Copy the base ID from your Airtable URL (starts with "app")
   - Copy the table ID (starts with "tbl")

### Step 3: Import Workflow to n8n

1. **Access Your n8n Instance**:
   - Log into your n8n dashboard

2. **Import the Workflow**:
   - Click "New" → "Import from JSON"
   - Paste the provided JSON workflow
   - Click "Import"

### Step 4: Configure API Credentials

1. **Set Up Airtable Connection**:
   - Click on the "Airtable Storage" node
   - Click "Create new credential"
   - Name it "Airtable Personal Access Token account"
   - Enter your Airtable Personal Access Token
   - Test the connection

2. **Update Apify API Tokens**:
   - Click on "Reddit Post API call" node
   - Replace with your API token

### Step 5: Configure Search Parameters

1. **Customize Search Settings**:
   - Click on "Search Parameters" node
   - Modify these values as needed:
     - `query`: Change "content creation workflow code included" to your desired search terms
     - `subreddit`: Change "n8n" to your target subreddit (without r/)

2. **Example Alternative Configurations**:
   ```
   Query: "lead generation workflow code included"
   Subreddit: "automation"
   
   Query: "github repository open source"
   Subreddit: "selfhosted"
   ```

### Step 6: Adjust Schedule for Production

1. **Modify Schedule Trigger**:
   - Click on "Schedule Trigger" node
   - **IMPORTANT**: Change from 1 minute to a more reasonable interval
   - Recommended settings:
     - Every hour: Set to 60 minutes
     - Daily: Set to 24 hours
     - This prevents API rate limiting

### Step 7: Test the Workflow

1. **Manual Test**:
   - Click "Execute Workflow" button
   - Check each node for successful execution
   - Green checkmarks indicate success

2. **Verify Data Flow**:
   - Check that Reddit posts are being fetched
   - Ensure filtering is working (only posts with GitHub/YouTube/Google Drive links)
   - Confirm data is being saved to Airtable

3. **Check Airtable**:
   - Go to your Airtable base
   - Verify that Reddit posts are appearing in your table
   - Check that all fields are populated correctly

### Step 8: Activate Workflow

1. **Enable Auto-Execution**:
   - Toggle the workflow to "Active"
   - The schedule trigger will now run automatically

2. **Monitor Performance**:
   - Check execution logs regularly
   - Monitor API usage on Apify dashboard
   - Watch for any error notifications

---

## Troubleshooting

### Common Issues:

1. **API Rate Limits**:
   - Increase schedule interval
   - Check Apify usage quotas
   - Consider upgrading Apify plan if needed

2. **No Results Found**:
   - Adjust search query terms
   - Try different subreddits
   - Check if the target subreddit has recent posts

3. **Airtable Connection Errors**:
   - Verify Personal Access Token permissions
   - Check base and table IDs are correct
   - Ensure field names match exactly

4. **Apify Actor Errors**:
   - Verify actor URLs are accessible
   - Check if actors require updated parameters
   - Try running actors directly on Apify to test

### Performance Optimization:

1. **Reduce API Calls**:
   - Increase schedule intervals
   - Limit search results where possible
   - Use more specific search queries

2. **Filter Efficiency**:
   - The workflow filters for posts containing:
     - GitHub links: `github.com/`
     - YouTube links: `youtube.com/` or `youtu.be/`
     - Google Drive: `drive.google.com/`
     - Google Docs: `docs.google.com/`

---

## Customization Options

### Search Query Ideas:
- `"automation tool workflow share"`
- `"open source project github"`
- `"workflow template download"`
- `"integration tutorial code"`

### Alternative Subreddits:
- `nocode` - No-code community
- `automation` - General automation tools
- `selfhosted` - Self-hosted solutions
- `opensource` - Open source projects
- `productivity` - Productivity tools

### Additional Filters:
You can modify the "Filter for workflow Links" node to include other link types like:
- Notion templates
- Zapier workflows
- Medium articles
- Personal websites

---

## Expected Output

The workflow will create Airtable records with:
- **Reddit Username**: Post author
- **Post Title**: Original Reddit post headline
- **Post Body**: Full text content
- **Engagement Metrics**: Upvotes, comments, upvote ratio
- **Direct Link**: URL to the original Reddit post

This creates a valuable database of community-shared resources and workflows that you can reference, analyze, and potentially implement in your own projects.



## Share your feedback
suhaibnord@gmail.com
