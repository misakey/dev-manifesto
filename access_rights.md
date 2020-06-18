# Tools access rights

We follow the rule of the least access rights (https://en.wikipedia.org/wiki/Principle_of_least_privilege)

If you feel you need more access right, ask for them it won't be a problem, but it won't be present by default.

## 2FA Policy

We want to use 2FA everywhere it's possible. We provide to everyone a Yubikey to make it simpler. 

Here the list of tools where 2FA is mandatory:
- Gitlab (Yubikey & OTP available)
- Google Suite (Yubikey & OTP available)
- AWS (Yubikey OR OTP available)
- OVH (Yubikey OR OTP available)
- Bitwarden (Yubikey & OTP available - Require premium account, ask us to have it)
- Sentry (Yubikey & OTP available)
- Matomo (OTP Only for now)
- NPM (OTP Only for now)
- Webflow (OTP Only for now)

If you find a tool we're using that is not here, please propose a MR to add it !