# Duo Integration Pack

This pack integrates with Duo (was Duo Security), to allow 2FA to be
carried out within flows (everything except SMS is supported, but
defaults to auto).

## Auth Configuration 

Copy the example configuration in [duo.yaml.example](./duo.yaml.example)
to `/opt/stackstorm/configs/duo.yaml` and edit as required.

You need an application integration configured in the Duo interface.
Configure the ikey, skey and host in `duo.yaml`

```yaml
auth_host: api-hostname
auth_ikey: auth-api-integration-key
auth_skey: auth-api-secret-key
```

## Admin Configuration

To support feature actions, you can configure an admin API
key, however this is not currently used.

```yaml
admin_host: api-hostname
admin_ikey: admin-api-integration-key
admin_skey: admin-api-secret-key
```

## Actions

### duo.auth_ping

Confirms if the configured host is up.

### duo.auth_check

Confirms if the configured host, ikey and skey are valid.

### duo.auth_auth

Carries out an authentication against Duo for the user (defaults to
`{{action_context.api_user}}`) and `auto` for the factor.

It's possible to use passcode if you collect the passcode from the
user in a secure manner.

Although `SMS` is a valid factor it's not included as it automatically
denies the authentication and the user needs to be re-authed.
