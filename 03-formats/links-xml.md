---
id: format-links-xml
title: links_xml
type: format
status: draft
last_verified: 2026-10-30
used_by_tools: [enable_links]
---

# links_xml

## Full structure (as known)
```xml
<xml>
  <links>
    <link>
      <uri>DOMAIN/SERVICE</uri>   <!-- target, short domain name, no root domain -->
      <active>true</active>       <!-- true to enable -->
    </link>
    <!-- more <link> elements for more targets (TODO: confirm) -->
  </links>
</xml>
```

## Verified example
```xml
<xml><links><link><uri>production-domain/ttservice</uri><active>true</active></link></links></xml>
```

## Common mistakes
- Stray characters in the URI (e.g. a trailing `'`) are not rejected; the link may point nowhere.

## TODO
- Does `<active>false</active>` disable an existing link?
- Can `uri` point to another root domain?
