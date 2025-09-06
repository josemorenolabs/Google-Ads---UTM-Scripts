# Google Ads Script — Set `{_campaignname}` Custom Parameter

Updates the **custom URL parameter** for every campaign (Search, Display, and Video) in a Google Ads account so you can reference the campaign name in tracking templates via `{_campaignname}`.

## What this script does

- Loops through **all campaigns** using `AdsApp.campaigns()` and `AdsApp.videoCampaigns()`
- Sets a custom parameter named `campaignname` to each campaign’s current name
- Writes a log line for each updated campaign

```javascript
function main() {
  var campaigns = AdsApp.campaigns().get();
  updateCustomParameters(campaigns);

  var videoCampaigns = AdsApp.videoCampaigns().get();
  updateCustomParameters(videoCampaigns);
}

function updateCustomParameters(campaigns) {
  while (campaigns.hasNext()) {
    var campaign = campaigns.next();
    var campaignName = campaign.getName();

    campaign
      .urls()
      .setCustomParameters({ campaignname: campaignName });

    Logger.log('Updated {_campaignname} for campaign: ' + campaignName);
  }
}
