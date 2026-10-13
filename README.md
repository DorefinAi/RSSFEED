# Vartmaan AI News Wire - RSS Feed Deployment

Feed URL after deploy: https://wire.dorefinai.com/feed.xml  (replace with your subdomain)

## Files
- feed.xml     the RSS feed (UTF-8, no BOM, <?xml first line)
- vercel.json  serves feed.xml as application/xml; charset=utf-8
- index.html   simple landing page with feed autodiscovery link
- nginx.conf   alternative if self-hosting on a VPS

## Deploy on Vercel
1. git init && git add . && git commit -m "rss feed"
2. Push to a new GitHub repo.
3. Vercel -> Add New -> Project -> import repo -> Framework: Other -> Deploy.
4. Project -> Settings -> Domains -> add wire.dorefinai.com
5. At your DNS provider add:  CNAME  wire  ->  cname.vercel-dns.com
   (use the exact value Vercel shows; on Cloudflare set DNS only / grey cloud)
6. Wait for "Valid Configuration" + SSL.

## Verify
curl -I https://wire.dorefinai.com/feed.xml
Expect 200 and content-type: application/xml; charset=utf-8
Validate at https://validator.w3.org/feed/

## Updating
Every new story needs a unique <guid> and updated <lastBuildDate>.
Commit the new feed.xml to GitHub and Vercel auto-deploys.
(An n8n workflow can do this with the GitHub node.)

## Note
<link> URLs in items point to https://dorefinai.com/wire/... - make those
pages exist or change them to your subdomain.
