# Automation Details

## GitHub Action Workflow

This repository uses a GitHub Action to automatically sync the Civ V - Vanilla ruleset from the main Unciv repository.

### Workflow: `sync-ruleset.yml`

**Triggers:**
- Scheduled: Runs daily at midnight UTC (cron: `0 0 * * *`)
- Manual: Can be triggered manually from the GitHub Actions tab using workflow_dispatch

**Steps:**
1. **Checkout**: Checks out this repository
2. **Clone Unciv**: Clones the latest version of the Unciv repository
3. **Copy Ruleset**: Copies all files from `android/assets/jsons/Civ V - Vanilla/` to `jsons/`
4. **Create PR**: Creates a pull request with any changes detected

**Safety Features:**
- The workflow does NOT run on push events to prevent infinite loops
- Uses peter-evans/create-pull-request to safely handle updates
- Deletes the sync branch after PR is merged

## Manual Testing

To test the sync process locally:

```bash
# Clone Unciv
git clone --depth 1 https://github.com/yairm210/Unciv.git /tmp/Unciv

# Copy ruleset
mkdir -p jsons
cp -r /tmp/Unciv/android/assets/jsons/Civ\ V\ -\ Vanilla/* jsons/

# Clean up
rm -rf /tmp/Unciv
```

## Mod Structure

This repository follows the Unciv mod format:
- `jsons/` - Contains all ruleset JSON files
- `.github/workflows/` - Contains automation workflows
- `README.md` - Documentation for users
- `.gitignore` - Excludes build artifacts and IDE files

## Source Information

- **Source Repository**: https://github.com/yairm210/Unciv
- **Source Path**: `android/assets/jsons/Civ V - Vanilla/`
- **Format Reference**: https://github.com/yairm210/Unciv-mod-example
