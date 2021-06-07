# Request for Custom Domain Support

Since our Kutt instance is hosted on [Railway](https://railway.app), we need an way for our users in our instance to make their custom
domains work like magic without facing the `404 Not Found` issue.

## Prerequisite

* You should added your custom domain into your account, preferrbly on an subdomain.
* Your custom domain should point into either one of our instances, depending on where you saved it:
  * `rtapp.tk` - for production instance, which we recommend to point to
  * `dev.rtapp.tk` - for dev instance, where deployments from the `develop` branch happens. (not recommended for normal usage)
* When pointing your DNS records for your custom domain to our Kutt instance, it should be either an `CNAME` or `ANAME` (or `ALIAS`, this might depends on your DNS provider) record. For Cloudflare users, you should orange-cloud the apex domain record to automatically flatten CNAMEs.
  * Otherwise, you should switch to an DNS provider that either supports `ANAME`/`ALIAS` records or CNAME flattening. If you want to let us manage your DNS records in Cloudflare (wbich provided free of charge), [create one here](https://rtapp.tk/cl) (skip if you have one) and add `custom-domains-support@rtapp.tk` as an admin. (You can also request one to be managed by us, but you need to export your DNS records first.)

### Managing DNS records on us

If you want Cloudflare's CNAME flattening, our nameservers are:

* `reserved.ns.cloudflare.com`
* `reserved.ns.cloudflare.com`

_These nameservers may update, [you should subscribe to this issue](https://github.com/RecapTime/rtappdotio-custom-domains/issues/1) for updates._

While managing DNS on us is free of charge, we might nicely ask to [support us](https://donate.madebythepins.tk) to keep this service up and to afford the Pro plan for managed DNS customers in the future.

If your custom domain is probably not on apex domain, you can manage your DNS records on us through Netlify. Please let us know about that in your request.

## How to Request

1. [Use this issue template][link] to submit an request. Remember to fill up these required fields:
    * Custom domain
    * Configured homepage
    * Mailhide.io link for your email address (e.g. <https://mailhide.io/e/7GZI6xKP>) or your public email address on your GitHub profile
    * DNS provider preference (currently Cloudflare and Netlify only)
    * Your digital signature (by signing off at end of the issue description or fill up the form locally and sign with PGP/Keybase) as your acceptance of the [ToS](https://rtapp.tk/terms).

[link]: https://github.com/RecapTime/rtappdotio-custom-domains/issues/new/choose

```markdown
<!-- this sign-off will be used to confirm acceptance of our ToS -->
Signed-off-by: Full Name Here <public-git-address@here.dev>

<!-- you may also copy the template source file, edit it and sign
     using your PGP key instead or in combination of signing-off.
     You may don't need this if you use Keybase to sign the form.-->
-----PGP SIGNATURE START----
...
----PGP SIGNATURE END-----
```

2. An team member with access to our shared GitHub account (`ThePinsTeam`) will add that domain into Railway project's custom domains for an specific environment you picked. If the form is not filled so much, we may asked you to add an TXT record for manual ownership verification purposes, similar to this format:

```txt
your.custom.domain TXT rtappdotio-custom-domain.code=<base64 stuff here, which staff may generate from random text> rtappdotio-environment.railwayapp=<rtappdotio|rtappdotio-development> rtapp-custom-domain.ghIssue=https://github.com/RecapTime/rtappdotio-custom-domains/issues/ISSUE-NUMBER-HERE
```

3. Voila! We'll check within few days to confirm it's working through DNS record lookup and 404-not-found checker. Enjoy your new custom domain. (We may do DNS record checks periodically to ensure it's actively using)

4. If you want to self-host our fork of Kutt, here's [our source code](https://rtapp.tk/source). Remember to export your existing shortlinks first! (Stats not included to be availale for data exports, sadly.) Remove your custom domain's CNAME/ANAME and TXT record (or change it) and we'll remove it from the project dashboard.
