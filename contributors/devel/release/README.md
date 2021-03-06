This document captures the requirements and responsibilities of the individuals responsible for Kubernetes releases.

As documented in the [Kubernetes Versioning doc](https://github.com/kubernetes/kubernetes/blob/master/docs/design/versioning.md), there are 3 types of Kubernetes releases:
* Major (x.0.0)
* Minor (x.x.0)
* Patch (x.x.x)

Major and minor releases are managed by a **Kubernetes Release Management Team**, and patch releases are managed by the **Patch Release Manager**. Exact roles and duties are defined below.

# Patch Release Manager

Patch releases are managed by the **Patch Release Manager**. Duties of the patch release manager include:
* Ensuring the release branch (e.g. `release-1.5`) remains in a healthy state.
  * If the build breaks or any CI for the release branch becomes unhealthy due to a bad merge or infrastructure issue, ensure that actions are taken ASAP to bring it back to a healthy state.
* Reviewing and approving [cherry picks](https://github.com/kubernetes/community/blob/master/contributors/devel/cherry-picks.md) to the release branch.
  * Patch releases should not contain new features, so ensure that cherry-picks are for bug/security fixes only.
  * Cherry picks should not destabilize the branch, so ensure that either the PR has had time to stabilize in master or will have time to stabilize in the release branch before the next patch release is cut.
* Setting the exact schedule (and cadence) for patch releases and actually cutting the [releases](https://github.com/kubernetes/kubernetes/releases).

Current and past patch release managers are listed [here](https://github.com/kubernetes/community/wiki).

# Kubernetes Release Management Team for Major/Minor Releases

Major and Minor releases are managed by the **Kubernetes Release Management Team** which is responsible for ensuring Kubernetes releases go out on time (as scheduled) and with high quality (stable, with no major bugs).

Roles and responsibilities within the Kubernetes Release Management Team are as follows.

#### Release Management Team Lead
The Release Management Team Lead is the person ultimately responsible for ensuring the release goes out on-time with high-quality.  All the roles defined below report to the Release Management Team Lead.
* Establishes and communicates responsibilities and deadlines to release management team members, developers/feature owners, SIG leads, etc.
* Escalates and unblocks any issue that may jeopardise the release schedule or quality as quickly as possible.
* Finds people to take ownership of any release blocking issues that are not getting adequate attention.
* Keeps track of, and widely communicates, the status of the release (including status of all sub-leads, all release blockers, etc) and all deadlines leading up to release.
* Manages [exception](https://github.com/kubernetes/features/blob/master/EXCEPTIONS.md) process for features that want to merge after code freeze.

#### Release Branch Manager
* Manages (initiates and enforces) code freeze on main branch as scheduled for the release.
  * Ensures no new features are merged after code complete, unless they've been approved by the [exception process](https://github.com/kubernetes/features/blob/master/EXCEPTIONS.md).
* Cuts the `release-x.x` branch at the appropriate time during the milestone.
* Ensures release branch (e.g. `release-1.5`) remains in a healthy state for the duration of the major or minor release.
  * If the build breaks, or any CI for the release branch becomes unhealthy due to a bad merge or infrastructure issue, ensures that actions are taken ASAP to bring it back to a healthy state.
* Initiates automatic fast-forwards of the release branch to pick up all changes from master branch, when appropriate.
* Reviews and approves [cherry picks](https://github.com/kubernetes/community/blob/master/contributors/devel/cherry-picks.md) to the release branch.
  * Ensures onlyl bug/security fixes (but no new features) are cherry-picked after code complete unless approved by the [exception process](https://github.com/kubernetes/features/blob/master/EXCEPTIONS.md).
  * Ensures that cherry-picks do not destabilize the branch by either giving the PR enough time to stabilize in master or giving it enough time to stabilize in the release branch before cutting the release.
* Cuts the actual [release](https://github.com/kubernetes/kubernetes/releases).

#### Release Docs Lead
* Sets release docs related deadlines for developers and works with Release Management Team Lead to ensure they are widely communicated.
* Sets up release branch for docs.
* Pings feature owners to ensure that release docs are created on time.
* Reviews/merges release doc PRs.
* Merges the docs release branch to master to make release docs live as soon as the release is official.

#### Release Notes Lead
* Compiles the major themes, new features, known issues, actions required, notable changes to existing behavior, deprecations, etc. and edits them into a release doc checked in to the feature repository (ready to go out with the release).

#### Bug Triage Lead
* Figures out which bugs (whether manually created or automatically generated) should be tracked for the release.
* Ensures all bugs being tracked for the release have owners that are responsive.
* Ensures all bugs are triaged as blocking or non-blocking.
* Ensures all bugs that are blocking are being actively worked on, esp after code complete.

#### Test Infra Lead
* Sets up and maintains all CI for the release branch.

#### Automated Upgrade Testing Lead
* Ensures that automated upgrade tests provide a clear go/no-go signal for the release.
* Tracks and finds owners for all issues with automated upgrade tests.

#### Manual Upgrade Testing Lead
* Ensures that any gaps in automated upgrade testing are covered by manual upgrade testing.
* Organizes the manual upgrade testing efforts, including setting up instructions for manual testing, finding manual testing volunteers, and ensuring any issues discovered are communicated widely and fixed quickly.

#### Testing Lead
* Ensures that all non-upgrade test CI provides a clear go/no-go signal for the release.
* Tracks and finds owners to fix any issues with any (non-upgrade) tests.
