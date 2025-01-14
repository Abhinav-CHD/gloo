
---
title: "jwt.proto"
weight: 5
---

<!-- Code generated by solo-kit. DO NOT EDIT. -->


### Package: `jwt.options.gloo.solo.io` 
#### Types:


- [JwtStagedVhostExtension](#jwtstagedvhostextension)
- [JwtStagedRouteExtension](#jwtstagedrouteextension)
- [VhostExtension](#vhostextension)
- [RouteExtension](#routeextension)
- [Provider](#provider)
- [Jwks](#jwks)
- [RemoteJwks](#remotejwks)
- [LocalJwks](#localjwks)
- [TokenSource](#tokensource)
- [HeaderSource](#headersource)
- [ClaimToHeader](#claimtoheader)
  



##### Source File: [github.com/solo-io/gloo/projects/gloo/api/v1/enterprise/options/jwt/jwt.proto](https://github.com/solo-io/gloo/blob/master/projects/gloo/api/v1/enterprise/options/jwt/jwt.proto)





---
### JwtStagedVhostExtension



```yaml
"beforeExtAuth": .jwt.options.gloo.solo.io.VhostExtension
"afterExtAuth": .jwt.options.gloo.solo.io.VhostExtension

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `beforeExtAuth` | [.jwt.options.gloo.solo.io.VhostExtension](../jwt.proto.sk/#vhostextension) | JWT Virtual host config for the JWT filter that runs before the extauth filter. |
| `afterExtAuth` | [.jwt.options.gloo.solo.io.VhostExtension](../jwt.proto.sk/#vhostextension) | JWT Virtual host config for the JWT filter that runs after the extauth filter. |




---
### JwtStagedRouteExtension



```yaml
"beforeExtAuth": .jwt.options.gloo.solo.io.RouteExtension
"afterExtAuth": .jwt.options.gloo.solo.io.RouteExtension

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `beforeExtAuth` | [.jwt.options.gloo.solo.io.RouteExtension](../jwt.proto.sk/#routeextension) | JWT route config for the JWT filter that runs after the extauth filter. |
| `afterExtAuth` | [.jwt.options.gloo.solo.io.RouteExtension](../jwt.proto.sk/#routeextension) | JWT route config for the JWT filter that runs after the extauth filter. |




---
### VhostExtension



```yaml
"providers": map<string, .jwt.options.gloo.solo.io.Provider>
"allowMissingOrFailedJwt": bool

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `providers` | `map<string, .jwt.options.gloo.solo.io.Provider>` | Map of JWT provider name to Provider. If specified, multiple providers will be `OR`-ed together and will allow validation to any of the providers. |
| `allowMissingOrFailedJwt` | `bool` | Allow pass through of JWT requests for this virtual host, even if JWT token is missing or JWT auth failed. If this is false (default false), requests that fail JWT authentication will fail authorization immediately. For example, if a request requires either JWT auth OR another auth method, this can be enabled to allow a failed JWT auth request to pass through to the other auth method. |




---
### RouteExtension



```yaml
"disable": bool

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `disable` | `bool` | Disable JWT checks on this route. |




---
### Provider



```yaml
"jwks": .jwt.options.gloo.solo.io.Jwks
"audiences": []string
"issuer": string
"tokenSource": .jwt.options.gloo.solo.io.TokenSource
"keepToken": bool
"claimsToHeaders": []jwt.options.gloo.solo.io.ClaimToHeader
"clockSkewSeconds": .google.protobuf.UInt32Value

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `jwks` | [.jwt.options.gloo.solo.io.Jwks](../jwt.proto.sk/#jwks) | The source for the keys to validate JWTs. |
| `audiences` | `[]string` | An incoming JWT must have an 'aud' claim and it must be in this list. |
| `issuer` | `string` | Issuer of the JWT. the 'iss' claim of the JWT must match this. |
| `tokenSource` | [.jwt.options.gloo.solo.io.TokenSource](../jwt.proto.sk/#tokensource) | Where to find the JWT of the current provider. |
| `keepToken` | `bool` | Should the token forwarded upstream. if false, the header containing the token will be removed. |
| `claimsToHeaders` | [[]jwt.options.gloo.solo.io.ClaimToHeader](../jwt.proto.sk/#claimtoheader) | What claims should be copied to upstream headers. |
| `clockSkewSeconds` | [.google.protobuf.UInt32Value](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/u-int-32-value) | Optional: ClockSkewSeconds is used to verify time constraints, such as `exp` and `npf`. Default is 60s. |




---
### Jwks



```yaml
"remote": .jwt.options.gloo.solo.io.RemoteJwks
"local": .jwt.options.gloo.solo.io.LocalJwks

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `remote` | [.jwt.options.gloo.solo.io.RemoteJwks](../jwt.proto.sk/#remotejwks) | Use a remote JWKS server. Only one of `remote` or `local` can be set. |
| `local` | [.jwt.options.gloo.solo.io.LocalJwks](../jwt.proto.sk/#localjwks) | Use an inline JWKS. Only one of `local` or `remote` can be set. |




---
### RemoteJwks



```yaml
"url": string
"upstreamRef": .core.solo.io.ResourceRef
"cacheDuration": .google.protobuf.Duration
"asyncFetch": .solo.io.envoy.extensions.filters.http.jwt_authn.v3.JwksAsyncFetch

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `url` | `string` | The url used when accessing the upstream for Json Web Key Set. This is used to set the host and path in the request. |
| `upstreamRef` | [.core.solo.io.ResourceRef](../../../../../../../../../solo-kit/api/v1/ref.proto.sk/#resourceref) | The Upstream representing the Json Web Key Set server. |
| `cacheDuration` | [.google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration) | Duration after which the cached JWKS should be expired. If not specified, default cache duration is 5 minutes. |
| `asyncFetch` | [.solo.io.envoy.extensions.filters.http.jwt_authn.v3.JwksAsyncFetch](../../../../../external/envoy/extensions/filters/http/jwt_authn/v3/config.proto.sk/#jwksasyncfetch) | Fetch Jwks asynchronously in the main thread before the listener is activated. Fetched Jwks can be used by all worker threads. If this feature is not enabled: * The Jwks is fetched on-demand when the requests come. During the fetching, first few requests are paused until the Jwks is fetched. * Each worker thread fetches its own Jwks since Jwks cache is per worker thread. If this feature is enabled: * Fetched Jwks is done in the main thread before the listener is activated. Its fetched Jwks can be used by all worker threads. Each worker thread doesn't need to fetch its own. * Jwks is ready when the requests come, not need to wait for the Jwks fetching. |




---
### LocalJwks



```yaml
"key": string

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `key` | `string` | Inline key. this can be json web key, key-set or PEM format. |




---
### TokenSource

 
Describes the location of a JWT token

```yaml
"headers": []jwt.options.gloo.solo.io.TokenSource.HeaderSource
"queryParams": []string

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `headers` | [[]jwt.options.gloo.solo.io.TokenSource.HeaderSource](../jwt.proto.sk/#headersource) | Try to retrieve token from these headers. |
| `queryParams` | `[]string` | Try to retrieve token from these query params. |




---
### HeaderSource

 
Describes how to retrieve a JWT from a header

```yaml
"header": string
"prefix": string

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `header` | `string` | The name of the header. for example, "authorization". |
| `prefix` | `string` | Prefix before the token. for example, "Bearer ". |




---
### ClaimToHeader

 
Allows copying verified claims to headers sent upstream

```yaml
"claim": string
"header": string
"append": bool

```

| Field | Type | Description |
| ----- | ---- | ----------- | 
| `claim` | `string` | Claim name. for example, "sub". |
| `header` | `string` | The header the claim will be copied to. for example, "x-sub". |
| `append` | `bool` | If the header exists, append to it (true), or overwrite it (false). |





<!-- Start of HubSpot Embed Code -->
<script type="text/javascript" id="hs-script-loader" async defer src="//js.hs-scripts.com/5130874.js"></script>
<!-- End of HubSpot Embed Code -->
