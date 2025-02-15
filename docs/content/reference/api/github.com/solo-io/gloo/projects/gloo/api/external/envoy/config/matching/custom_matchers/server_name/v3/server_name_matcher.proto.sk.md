
---
title: "server_name_matcher.proto"
weight: 5
---

<!-- Code generated by solo-kit. DO NOT EDIT. -->


### Package: `envoy.config.matching.custom_matchers.server_name.v3` 
#### Types:


- [ServerNameMatcher](#servernamematcher)
- [ServerNameSetMatcher](#servernamesetmatcher)
  



##### Source File: [github.com/solo-io/gloo/projects/gloo/api/external/envoy/config/matching/custom_matchers/server_name/v3/server_name_matcher.proto](https://github.com/solo-io/gloo/blob/master/projects/gloo/api/external/envoy/config/matching/custom_matchers/server_name/v3/server_name_matcher.proto)





---
### ServerNameMatcher

 
Matches a specific server name provided in the client request against a set server names configured for the matcher to handle, with possible prefix wildcard.

```yaml
"serverNameMatchers": []envoy.config.matching.custom_matchers.server_name.v3.ServerNameMatcher.ServerNameSetMatcher

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `serverNameMatchers` | [[]envoy.config.matching.custom_matchers.server_name.v3.ServerNameMatcher.ServerNameSetMatcher](../server_name_matcher.proto.sk/#servernamesetmatcher) | Match server names. Order doesn't matter, the most specific server name is matched. |




---
### ServerNameSetMatcher

 
Specifies a list of server names and a match action.

```yaml
"serverNames": []string
"onMatch": .xds.type.matcher.v3.Matcher.OnMatch

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `serverNames` | `[]string` | A non-empty set of server names. Server name can start with a wildcard prefix, e.g. "*.example.com". |
| `onMatch` | [.xds.type.matcher.v3.Matcher.OnMatch](../../../../../../../xds/type/matcher/v3/matcher.proto.sk/#onmatch) | Match action to apply when the input matches the server name. |





<!-- Start of HubSpot Embed Code -->
<script type="text/javascript" id="hs-script-loader" async defer src="//js.hs-scripts.com/5130874.js"></script>
<!-- End of HubSpot Embed Code -->
