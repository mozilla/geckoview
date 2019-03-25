**Feature Name** Proposed RFC Process for Significant Changes to GeckoView's API

**Start Date** 25th March 2019

**Issue** https://github.com/mozilla/geckoview/issues/44

**Stage** Proposal

# Summary

A proposal to instigate an RFC (Request For Comments) process for significant changes to GeckoView's API. 

The proposed RFC process will consitute a template to provide structure to API changes, alongside a process for submitting a proposal for review, including guidelines for gathering feedback, entering a final review period, accepting the change and implementing the accepted proposal.

Also delivered as part of this proposal will be a guide to help proposers identify whether a change is considered significant enough to require an RFC and instructions on what how to submit an RFC.

# Motivation

In at least 3 recent instances GeckoView developers have made significant changes to the GeckoView API that have subsequently had to go through a period of review or discussion after the code has been written. 

1. When developing the Viewport Screenshot API, a decision was made to place the API inside `GeckoView` rather than `GeckoSession`, a decision that was unexpected by Android Components and caused them to have to rethink the way they presented the API to their consumers. Better communication with consumers ahead of the API design would have enabled a greater understanding of the decisions behind the API location and allowed consumers to prepare ahead of time for the API to land.
2. When designing the new Web Extensions APIs, serious attempts had been made before the code was written to ensure that all interested and affected parties were involved in the API design process. This was conducted using Need Information requests from inside Bugzilla. With many of the feedback requests from important parties going unanswered until code was available for review, significant changes had to be made that could have been avoided if the feedback requests had been successful.
3. Removing the `saveState` API required Android Components to rethink their session store as the API formed the basis for a lot of their design. Better communication with consumers ahead of the API design would have enabled a greater understanding of the decisions behind the API removal and allowed consumers to prepare ahead of time for the change to land.

All of these instances could have been avoided had there been an easier way to communicate significant API changes before the code was written and allowed a period to gather feedback on the proposed changes. Such a process allows the API designed to be better informed before development begins about the use cases and expectations of the consumers for APIs and signals significant changes ahead of time to consumers to allow them to better plan for when the changes land.

In addition, we are expecting to start recieving greater contributor attention through partnerships and greater publicity soon. We will need a way to curate and communicate upcoming changes to external consumers and ensure that we are building the right APIs for their needs. The RFC process will help us triage feature requests from third party contributors, communicate our roadmap and ensure that we are correctly collecting requirements for partners.

# Explanation

The proposed RFC process is as follows:

1. Deciding whether a proposed change requires an RFC.
    Only significant changes to the API should require an RFC. Significant changes are defined as changes that: 
    - Add new functionality to GeckoView.
    - Change the way the existing API works such that it affects its usage by consumers.
    - Remove functionality from the existing API.

2. Writing the proposal

    To write a proposal, a copy of `rfcs/_templates/rfc-template-000.md` should be taken, renamed to `<proposal-name>-<number>.md` and saved to `rfcs/`. 

    Each section in the template should be updated with the details for the proposal. The design of the template is twofold. Firstly it is designed to ensure that proposers have thought about all the details relevant to the proposal, such as who the proposal affects, how it will work and the risks, uncertainties and unknowns involved. 

    Secondly, the template is designed to give as many answers to questions that reviewers have in advance, and to provide advanced notice to consumers such that they can prepare for the eventual landing of the proposed change.

    Advice on writing the proposal should be presented in a `README.md` inside `rfcs`. This advice should include requesting proposers gather feedback on their proposal from other members of their team to ensure that they have covered all their use cases and that their argument is sound before submitting the proposal for review. If the proposer wants to conduct this early team review through GitHub, they should submit a PR with their proposal and add `WIP` in front of the PR title and add the `Work In Progress` label to the PR. Reviewers should refrain from providing feedback on `WIP` proposals until they are explicitly asked to review. 

3. Submitting the proposal for review

    Once the proposal template has been completed, a PR should be raised with containing the proposal document along with any supporting documentation that the proposal needs. Supporting documentation can take the form of code samples, draft documentation, example usages or proposed timelines according to the content of the proposal.

    If a `WIP` proposal is already raised for the proposal, the `WIP` should be removed from the title and the `Work in Progress` label should be removed from the PR. 

    The PR should be labeled with the `RFC` label. Proposers should ensure they have assigned the PR to themselves if they are a member of the repo team. If they are not a team member, the PR comments should include the proposers details, including the team they are on (if Mozilla) or whether they are a partner or a contributor, and how they are consuming GeckoView.

    The PR Title should be the same as the title included in the proposal document. 

    Critical reviewers should be named in the description of the PR alongside a checkbox. Critical reviewers are reviewers without whose agreement the proposal cannot be accepted. If new critical reviewers are discovered during the review process, their names should be added at that time.

    Once the PR has been submitted, a link to the proposal PR should be added in a comment to the Bugzilla or Github issue

4. Requesting feedback on the proposal
    After submitting the PR containing the proposal and any supporting documents, the GeckoView team should be added to the list of reviewers. All proposals must include the GeckoView team as reviewers. Proposals that have not been reviewed by the GeckoView team will not be accepted.

    If there are other interested parties who also need to review the proposal, they should also be included in the reviewers. If the interested party is not on GitHub then the following methods should be used to request feedback:

    - Email reviewer directly and request feedback giving link to PR.
    - Add link to PR to the Bugzilla issue and NI that reviewer from there.
    - Contact the reviewer through Slack or IRC and request that they review the proposal.

    Advice should be provided in the `README.md` inside `rfcs` to instruct proposers to make clear the importance of the feedback for the issue when contacting a reviewer directly. If the reviewer has been identified as a Critical Reviewer then any communication should include the fact that the reviewers feedback is required before the proposal can be accepted.

5. Responding to feedback on the proposal

    On receipt of feedback on a proposal, the proposal should be updated to take the feedback into account. This can be done either as a new commit or amending the original commit to include the changes. The reviewer should be notified that their feedback has been addressed. Responding to their comment on the PR should be sufficient.

6. Entering the final review phase

    Once all critical reviewers have reviewed the proposal, the proposal should enter the final review phase. The title of the PR should be updated to include `Final Review` and the `Final Review` label should be added to the PR.

    Once a proposal has hit Final Review, it will be open for comments for a further 24 hours. All reviewers should be notified that the proposal has entered this phase. At the end of this period no further comments or amendments should be made to the proposal. 

7. Accepting/Rejecting the proposal
    
    At the end of the `Final Review` period, Critical Reviewers are asked to either "accept" or "reject" the proposal by checking the box next to their names in the PR description. If the proposal is accepted then it should be merged so that the proposal appears in a list of "Accepted" RFCs. The proposal is now "Active".

    If the proposal is rejected then the PR is commented on to indicate the rejection and is closed. The proposal PR and associated branch should not be deleted so that it can be referred to at a later date in case a similar or related proposal is submitted.

    "Active" proposals should be available to view and search from the GeckoView website.

8. Implementing the proposal

    During implementation of an accepted proposal, reviewers and developers should refer to the proposal to ensure that the delivered solution matching the requirements specified in the proposal.

9. Delivering the proposal

    Once the implementation for a proposal has landed, the proposal document should be moved into the "Complete" subfolder. Complete proposals should be available to view and seach from the GeckoView website.

# Technical Specification

- [Proposal Template] (_templates/rfc-template-0000.md).
- [RFC guide](README.md)
- Proposed directory structure:
```
    | rfcs
    __ 
        | _templates
        __  | rfc-template-0000.md
        | complete
        __  | index.md
            | `list of complete RFCs`
        | index.md
        | `list of active RFCs.`
```

# Problems

It may be difficult to gather feedback from non-Github users. If Bugzilla and email is also used as a way to gather feedback then it may be difficult to cross reference feedback from multiple sources.


# Unknowns

It is unknown how long a typical proposal review cycle will take. It is possible that it will take longer than our development timescales have room to factor in. A more lightweight process may be required for changes identified as "significant" but that are "quick" to implement.

# Alternatives and Rationale

I have chosed GitHub as the platform for hosting the RFC process for several reasons.

1. The structure of the PR submission and review process is collaborative and easy to use. Viewing feedback and responding to it is simple to understand.
2. Branches make the process of writing and submitting the proposals very separate from the live site, making it easy to have multiple proposals on the go.
3. The use of labels makes it easy to see the stage of review a proposal is in.
4. Many partners and collaborators are already familiar with GitHub and how it works.
5. The closeness of the RFC area to the GeckoView website means moving a proposal to being publicly visible is easy.
6. PRs are very searchable.

The considered alternatives were:

- Google Docs style solution 
    - Proposal in Google Docs, emailed around to reviewers.
    - Makes presentation of in the proposal lifecycle publicly difficult (cannot easily be mirrored to the website).
    - Makes searching for related or existing proposals hard.
- Place the RFC template and proposal documents in mozilla-central and use Bugzilla/Phabricator for review requests.
    - Not good for long term
    - Searchability is low
    - Would need to shadow to gh-pages to get a public interface.

# Prior Art

[Swift Evolution](https://apple.github.io/swift-evolution/)
[Rust RFC](https://github.com/rust-lang/rfcs)

# Future Developments

Unknown.
