# Agent Registration

This service supports agent-assisted registration for School of Freelancing.

## Discovery

Agents should first fetch:

- Protected Resource Metadata: `https://www.schooloffreelancing.com/.well-known/oauth-protected-resource`
- Authorization Server Metadata: `https://www.schooloffreelancing.com/.well-known/oauth-authorization-server`

The Authorization Server metadata contains the `agent_auth` registration metadata and the canonical registration URI.

## Supported flow

### Anonymous registration

The service supports an anonymous registration flow. The agent may create a School of Freelancing account through the published registration endpoint without presenting a third-party identity assertion.

- Identity type: `anonymous`
- Credential type: `access_token`
- Registration method: `POST`
- Registration URI: `https://www.schooloffreelancing.com/auth/register`

Agents must request only the minimum access required and must not expose credentials to third parties.

## Registration

1. Fetch the OAuth Protected Resource Metadata.
2. Fetch the Authorization Server Metadata and read the `agent_auth` block.
3. Use the advertised `register_uri` and supported identity type.
4. Submit only the fields required for account registration.
5. Treat any issued credential as sensitive and use it only for the permissions granted by the service.

## Claim and revocation

No separate claim or revocation URI is published for this anonymous registration profile at this time. Agents should treat authentication failures or revoked credentials as a signal to stop using the credential and restart discovery/registration according to the service's current metadata.

## Security

Use HTTPS only. Do not transmit passwords or credentials to any host other than `www.schooloffreelancing.com`. Do not log credentials, and do not reuse credentials outside their intended School of Freelancing account.
