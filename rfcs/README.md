# GeckoView RFC Process

Changes to the GeckoView API that impact consumers are considered "significant" changes. We try to make sure that our APIs are the best that they can be, and in order to ensure that significant changes must go through an RFC (Request For Comments) process. The process is here to provide structure, guidance and feedback on significant changes leading to APIs that are useful, understandable and easy to use.

The RFC process allows feedback to be gathered from all interested parties on well thought through and explained proposals for change.

If you want to make a change to GeckoViews APIs, if you can answer "yes" to any of these questions then your change is a "significant" change and you must submit an RFC before landing the change.

- Does your change allow access to a new feature, or make public a feature previously only available internally?
- Does your change change the behaviour of an existing API such that consumers would need to update their code in order to continue using the feature?
- Does your change remove existing functionality from users requiring them to use alternative methods to continue providing the same functionality to their users?

If you answered yes to any of these questions, please follow the RFC process outlined below to ensure that your change is accepted into GeckoView.

## The RFC Process

- Fork the GeckoView repository.
- Make a copy of the [RFC template](rfcs/_templates/rfc-template-000.md). 
- Rename the file to `<proposal-name>-0000.md`, where proposal-name is a short but descritive name for your proposal and save it under `rfcs/`. 
- Fill in the RFC document. Please ensure to fill it in carefully and flesh out as much detail as possible. 
    + You may wish to use the PR mechanism to gather early feedback from your team as a work in progress. If so, please add "WIP" to the front of the title of the pull request and add the "Work In Progress" label. Do not add any reviewers other than your team until your RFC is no longer a work in progress.
- Submit a pull request containing your RFC and any supporting documentation.
- Assign the PR to yourself.    
    + If you are unable to assign the PR to yourself, add your details, including the team you are working on, to the description section of the PR.
- Add the "RFC" label to the PR. Remove any "WIP" labels and title amendments.
- Add a link to any associated Bugzilla or Github issue in the PR description.
- Request review from the `GeckoView` team, plus any other interested parties as needed. Reach out to as many potential consumers of the API as you can. If your desired reviewer is not on GitHub, you can use the following methods to contact them:
    + Email reviewer directly and request feedback giving link to PR.
    + Add link to PR to the Bugzilla issue and NI that reviewer from there.
    + Contact the reviewer through Slack or IRC and request that they review the proposal.
- Respond to feedback. Update the PR with requested changes and inform reviewers that you have addressed their comments.
- At some point a member of the `GeckoView` team will move the RFC into "Final Review". This will have been done when any identified "Critical Reviewers", reviewers without whose agreement the RFC cannot be accepted, have signed off on the RFC. At this stage the remaining reviewers will have 24 hours to make further comments. By the time an RFC reaches final review, it is unlikely that any major issues will be surfaced. If they are, however, the "Final Review" period will be cancelled in order to allow the issue to be addressed.
- At the end of the "Final Review" period, the RFC will be either accepted or rejected.
    + If the RFC is accepted it will be merged so that the RFC appears in the list of "Active" RFCs on the GeckoView website. 
    + If the RFC is rejected then the PR will be closed. The RFC PR and associated branch should not be deleted so that it can be referred to at a later date in case a similar or related RFC is submitted.

# Implementing an Active RFC

- The person who submitted the RFC does not have to be the person who implements it.
- The RFC should be considered a requirements specification and will be used by reviewers to ensure that the submitted solution conforms.
- The code submisson and review process outlined in our [contributors guide](../tutorials/contributing-to-mc.md) should be followed when implementing an RFC. 
- Ensure that a link to the RFC document is added to the comments when submitting your solution to Phabricator.

# [Active RFCs](index.md)
# [Complete RFCs](complete/index.md)