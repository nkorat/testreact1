# Story: Prevent concurrent logins for the same user (first login wins)

## User story
As a security/compliance owner, I want a second login by the same user to be rejected while their first session is active, so that one account can't be used from two browsers or devices at the same time.

## Acceptance criteria
- A user logged in on browser A who logs in on browser B is redirected to a "session in use" page, and A is unaffected.
- This works for both SSO (SAML/OIDC) and form login.
- After A logs out or A's session times out, B can log in.
- When two logins happen at the same moment, exactly one succeeds.
- It works across all cluster nodes.
- Users with exempt roles (e.g. Administrator) can have concurrent sessions.
- Helpdesk can unlock a user immediately.
- Settings can be changed in System Settings without a redeploy (on/off, redirect URL, heartbeat, grace period, exempt roles, fail-open).

## Scope
- Shared DB registry (Service Builder table) with a lock per user.
- Login post-action that rejects the new login, a servlet filter for heartbeat and safety-net checks, and a session-destroy listener that releases the lock.
- A public "session in use" content page, owned by the content team.
- Groovy unlock script and a runbook.

## Out of scope
- "Last login wins" or a "sign out my other session" option.
- Limiting sessions at the IdP.
- Limiting headless API or token-based sessions.

## Dependencies and prerequisites
- `auth.simultaneous.logins` stays at its default (`true`), or Live Users stays off.
- The rejection page is public and must not trigger SSO, otherwise the browser loops.
- Sticky sessions on the load balancer.
- A DB schema change, which needs DBA review.

## Non-functional requirements
- No database access on most requests. There's one write per session per heartbeat interval (60s by default).
- If the database is down during login, behavior follows the fail-open/fail-closed setting. Established sessions are never kicked out.
- Log entries for rejections, including user ID and node, for audit.

## Known trade-offs and risks (agree with the product owner)
- A user who closes the browser without logging out is locked out for about the session timeout plus the grace period. Decide whether this is acceptable or whether the session timeout should be shorter.
- A node crash keeps the user locked until the lock expires.
- After rejection, the user's IdP session in browser B is still active.
- The code needs `javax` to `jakarta` changes when moving to 2025.Q3 or later.

## Open questions
- Which roles are exempt?
- Fail-open or fail-closed?
- What should the rejection page say, and should it be translated?
- What session timeout is acceptable?
- Is a self-service unlock needed later?
- Is helpdesk access to the unlock script approved?

## Test scenarios (for QA)
- Log in on A, then B: B is rejected.
- Log out on A, then log in on B: B succeeds.
- Close A without logging out: B is rejected until the timeout, or until a force unlock.
- Cluster: A on node 1, B on node 2: B is rejected.
- Two logins at the same moment.
- Kill A's node: B succeeds after the lock expires.
- An exempt-role user can log in twice.
- Registry DB unavailable: check both fail-open and fail-closed behavior.

## What drives the estimate
- Service Builder module and DB migration.
- SSO integration testing with the real IdP.
- Load testing on the cluster.
- Rejection page content and translation.
- Runbook.
