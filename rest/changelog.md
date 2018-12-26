# Cutwise Change Log

## 4.1.0

### API

- supported dedicated doman for API api.cutwise.com
- added External Diamonds API v3 (`/api/v3/diamond`)
- added Constants API v2 (`/api/v2/constants/{web/mobile/osv}`)
- added b2b list for filtering (`/api/v2/b2b/filters`)
- deprecated Filters API (`/api/v2/filters`), use Constants API v2 instead. This API will be removed in 4.3
- dropped `/messages/pushdebug`
- [BC] dropped `productTypes` and `fieldsMap` from deprecated Constants API v1
- [BC] dropped Notifications API
- [BC] dropped Saved Searches API
- [BC] dropped `b2b.showUnregistered` field
- [BC] dropped `b2b.disabledNotifications` field
- [BC] dropped `b2b.contactSeller` B2B relation
- [BC] dropped `/api/v2/metricsversions`
- [BC] dropped `/api/v2/productmetrics`
- [BC] dropped `cid` field from Product API
- [BC] dropped Filters API, use Constants API v2 instead
- [BC] dropped Constants API v1 (`/api/frontend/v1/constants`), use Constants API v2 instead

## 4.0.0

### API

- added User Stored Settings API
- added Collection API
- added Plottings API (`/api/v2/plottings`)
- added endpoint for OSV constants (`/api/v2/constants/osv`)
- [BC] `laboratory` in Product API now presented as id, please use dictionary to get titles
- [BC] `fluor.val` for Fluorescence metric changed to histogram n-f-m-s-vs
- [BC] symmetry metric attributes `hearts_val` renamed to `pav` and `asetw_val` renamed to `crown`
- supported integer Cutwise ProductID on Diamonds API
- [BC] `rough` property of diamond now appears as integer ID. Use additional request to retrieve rough is it necessary 
- [BC] dropped Facebook Bot support
- [BC] dropped Black Lists (/api/secured/v1/black_list/*)
- [BC] dropped Board API in favour of Collection API
- [BC] dropped Attribute API
- [BC] dropped Voting System API and entities
- [BC] dropped Distributions API 
- [BC] dropped some dictionary REST endpoints (`/api/v2/colors`, `/api/v2/clarities`, `/api/v2/cutqualities`, `/api/v2/mediasubformats`)
- [BC] dropped user photos (avatars)
- [BC] dropped endpoint `/api/v2/sharing/bulk`
- [BC] dropped `/share/{product_type}/{cid}` route in favour of `/share/{id}
- [BC] dropped `code` and `extTitle` from `cutShapes`
- [BC] dropped `/api/v2/purchases` Purchase API
- [BC] dropped `/api/v2/usercontacts` User Contacts API
- [BC] dropped `meta` HATEOAS embedded object from mediaSource
- [BC] field `inscriptions` in Diamond API is hidden
- [BC] removed `b2b` field from Product API, please use `seller` instead
- [BC] removed `purchaseStatus` and `purchaseStatusDetails` from Product API and Saved Search fitlers 
- [BC] removed `_cdn` from MediaSource
- [BC] removed `compare` block in Constants API
- [BC] removed duplicated `girdleThicknessMax` dictionary from Constants API
- [BC] removed `mediaSourceType` from mediaSource.
- [BC] removed `_isStandart` property from media. Use SetupPresets instead.
- [BC] removed `setupPreset` property in favour of `sp` prop with SetupPreset ID
- [BC] removed `preferMonochrome` property
- [BC] removed `mediaType` detalization. Only ID can appear now
- [BC] removed `code` from stone params like Clarity, Color, etc..
- [BC] removed `stones_media_colors` structure from constants, use bgColors instead
- [BC] removed `cutShape.extTitle` property
- [BC] removed `searchListState` from products
- [BC] removed `scale` from mediaSubFiles
- [BC] removed `user` from listing scope in `seller`
- [BC] supported authentification through the Bearer method via Authorization header (https://tools.ietf.org/html/rfc6749#section-7.1, https://tools.ietf.org/html/rfc6750)
- No more `/api/doc`

## 3.16.0

- added 'bgColors' array to constants response

## 3.13.0

- supported for AWS lifecycle
- ViBox scale ratio reduced by 2.60419705052445
- Added Cutwise Video Widget endpoint.

### DB

- dropped matrix_density table;
- dropped lighting_preset table;
- dropped fields source, meta, meta_external_url for media_source;
- dropped media_type_id from media_sub_formats;

### API

- added Artifacts storage REST
- added MetaData REST
- changed semantic of scaleRatio. Now it is a pixel size (in micrometres).
- [BC] removed field `data` from brightness metric.

## 3.12.0

### API

- collector V2 will not receive mediaId and setupPreset anymore;
- added `COPY /api/v2/board/{KEY}` method;
- added endpoint for bulk Saved Search product status change: `PUT /api/v2/searchlists/:searchListID/product/bulk`;
- added `setupPresetOrder` dictionary in constants;

### AWS

- changed restriction mode at S3 buckets. Now all fresh buckets have 'private' access mode by default;

## 3.10.2

- Added support of Dibox setup presets 

## 3.10.1

### API

- Added Optical Perfomance Per Area metric

## 3.10.0

### DB

- Dropped redundant `auth_code` table.
- Added `Other` base cut shape. 
- Dropped `Cart` related code

### API

- Import endpoint `POST /import/upload`. Accepts CSV/XLSX files with RapNet-compatible fields. More you can read in Cutwise Wiki
- Export `GET /export/download`. Takes products query-string parameter with ProductId list packed with Hashids lib (http://hashids.org/) with no salt. Second parameter is format (`csv`, `xlsx` or `html`). In this version only CSV format is production-ready.  
- Supported filtering and sorting for Cutwise OEM special fields. like: `&filters[oemFields][lotNumber]=404`

## 3.9.0

### API v2

- [BC] Dropped `isGeneralChild` property from cut shape entity. Proxy cut shapes was removed, now you should refer to base (root) cut shapes, not 'general child's ones.
- [BC] Dropped `agsCutGrade` and `certificateUrl` property from diamonds
- [BC] Properties `laboratory`, `labStatus`, `certufucateNumber`, `certificateFile` moved to new `certifications` collection in diamonds
- [BC] Dropped diamonds property `fire`, all containing data moved to HATEOAS `_embedded[metric.fire]` object!
- [BC] Dropped `metricMedia.mime` property
- [BC] Dropped `media.createdAt` property
- [BC] Dropped `[Product].isInIcart` property
- [BC] Dropped `[Product].isInBlack` property
- [BC] Dropped `mediaSource.media` property
- [BC] Dropped `metric.normalizedValue` property
- [BC] I3DReport links format changed to common Cutwise API HATEOAS format: `_links['report.show'].href`. This relations can be visible only in `detail` context.
- Deprecated property `product['_entityType']`. It will be removed in next versions.
- Added Certifications in all types of Product (with preview jpeg images 160x160).
- Added support of filters by 'lotNumber'
- Added Brilliancy and Average Brightness metrics, see `_embedded[metric.brightness]` in diamonds.
- Added Fluorescence metric, see `_embedded[metric.fluorescence]` in diamonds.
- Added Symmetry metric, see `_embedded[metric.symmetry]` in diamonds.
- Added support for DiBox2 Fluorescence image preset.
- Added any Product creation API (POST /avi/v2/diamonds{/roughs/jewelries}).
- Added relative datetime interval filter format with ISO 8601 duration format (https://en.wikipedia.org/wiki/ISO_8601#Durations). I.e.: filters[listed][rel]=P3W
- Added `scaleRation` property to mediaSource. `scale` property in subfiles is deprecated and will be removed in next versions.

### DB

- Dropped `name`, `description`, `site`, `createdAt`, `updatedAt` from `laboratory` table, `is_base` now NOT NULL, reduced `abbreviation` length.
- Dropped fields `certificate_url`, `ags_cut_grade` from diamonds.
- Dropped `normalizedvalue` from products_metrics.
- Dropped `meta` from search_lists.
- New table `certifications`.
- New materialized view `products_brightness_metrics`, with supporting triggers and procedures.
- New materialized view `products_fluorescence_metrics`, with supporting triggers and procedures.
- New materialized view `products_symmetry_metrics`, with supporting triggers and procedures.

## 3.8.0

### API v2

- Added REST CRUD for Boards
- Added PUT subscription block for Boards (without personal keys)
- Added external link to Boards in format /~{BoardId}
- Removed 'medias' property from Products API
- Dropped /api/frontend/v1/download/offline/page
- Dropped /api/frontend/v1/download/offline/page/videoSharing
- Dropped attribute attachOfflinePage on /api/frontend/v1/stones/send_video_sharing
- PurchaseStatusDetails has now strict DateTime format
- Changed PurchaseStatusDetails assoc from User to UserContact
- Added "scopes" array to filters output (now "listing" or "boards" values)
- Removed /api/frontend/v1/filters/{case}/{product_type} endpoint
- Added OEM Bundling
- Added oemFields JSON field in any products resource
- Created phpunit-debeers.xml for Running only Debeers tests
- Removed mediaStatus object from mediaCollection

### DB

- hardware and stage_hardware_type moved from LightingPreset to SetupPreset
- dropped orientation, diffusers, lighting, hdrMode and trajectory from LightingPreset
- dropped frameRate and frameCount from SetupPreset entity

## 3.7.0

### OAuth2 server

- Added access token lifetime client management
- Added stereoAngle in MediaSource resource
- Added preferMonochrome property in Media (both in data and form)
- Added Full CRUD for UserDeviceToken
- Added block 'connections' to server constants
- Added Facebook credentials to 'connection' block of server constants

## 3.6.0

### API v2

- Changed in b2b-user fields and relations structure
- Dropped B2B API (it was only traffic stats endpoint there)
- Dropped Stones v1 API
- Dropped fields emailNotificationInterval and pushNotificationInterval

### API methods added

- PUT: /api/v2/searchlists/{{id}}/notifications/{{type}}

### API methods changed

- PUT/POST: /api/v2/searchlists/{{id}} Now you can send notification settings in that entity, you must use special endpoint for them

### Entity changes

- Moved from to B2B: website, address, company, fax, contactPerson, title, opening, show_unregistered
- Removed from User: gender, description
- Fist and last name length in User entity is decreased to 128 chars.

## 3.5.0

### API v2

- Deprecated key-value format for list=true dictionaries in favor of array of objects (old behavior kept for b2b and rough endpoints).
- Added Google Oauth.
- Added meta data for mediaSource for product owners.
- Added ability to save base64 certificate file for diamonds
- Dropped CutShape unique constraint on title.
- Removed metaExternalUrl property from mediaSource
- Added Media.enabled property for Vendors (disabled property are shown on scope 'b2b').
- Added Manual order endpoint
- LabStatus field is removed from all forms and became virtual computed field

### DB additionals

- Added google_id for users.

### DB removals

- Dropped lab_status in diamonds.

## 3.4.0

### API v2

- Dropped `stoneShortView` attribute on products
- Dropped `b2bId` attribute on products
- Added `seller` attribute on products (for identifying seller — you should use this object). Inherits User entity intefrace. User entity in _b2b_ attribute will be deprecated.
- Added FULL CRUD for distributions
- Filter `b2bId` for product requests is deprecated (will be supported until 4.0). Use `b2b` instead
- Dropped API resource /api/frontend/v1/stonesbyids

### DB table removals

- Dropped created and updated fields from media_relevance.
- Dropped flags from media_sub_errors.

## 3.3.0

### API v2

- Removed property `cutwiseUrl` from products. Now this value can be retrieved from `_links[page.detail]`
- Added HATEOAS links for Products: share page and diamond detail page on frontend.

## 3.2.0

### API v2

- Removed property mediaCollection[n].mediaSources[k].mediaSourceType from products. SourceType can be retrieved at mediaCollection[n].setupPreset.mediaSourceType
- Added HATEOAS links to searchlists entities for metric charts link.
- Added scopes 'metrics' and 'compare'
- Added fire.details and metricsMedia objects for diamonds.

## 3.1.0

### API v2

- Added fire propery to diamond entity
- Added 3 fire.* sorting keys for diamond list
- Removed purchaseStatuses key from constants endpoint
- caratRanges property moved from constants to filters and renamed to caratGroups
- GET parameter entityType in filters v2 renamed to productType
- Totally reworked Filters v2
- All stone ext params moved to constants
- Constants method now supports "dropcache" query parameter

## 3.0.0

Totaly removed External Users functionality.
Temporary unsupported distributions.

### API methods removals

- GET /api/secured/v1/externals/{user_id}
- POST /api/secured/v1/externals/{user_id}
- PUT /api/secured/v1/externals/{user_id}
- GET /api/secured/v1/externals/{user_id}/stats
- GET /api/secured/v1/externals/{user_id}/{id}
- DELETE /api/secured/v1/externals/{user_id}/{id}
- POST /api/secured/v1/externals_batch_add/{user_id}
- POST /api/frontend/v1/stones/add_to_view_list
- POST /api/frontend/v1/stones/add_to_black_list
- POST /api/frontend/v1/external/activate
- POST /api/frontend/v1/external/preactivate
- POST /api/frontend/v1/external/add_device
- POST /api/frontend/v1/external/execute_action
- POST /api/frontend/v1/external/push_debug
- GET /api/frontend/v1/external/get_stone_list/{phone}
- POST /api/frontend/v1/stones/add_to_black_list
- GET /api/frontend/v1/download/offline/page/videoSharing/distribution
- GET /api/frontend/v1/distributions/{user_id}/{hash}
- GET /api/secured/v1/distributions/{user_id}
- GET /api/secured/v1/distributions/{user_id}
- POST /api/secured/v1/distributions/{user_id}/contact
- POST /api/secured/v1/distributions/{user_id}/comment/{id}
- DELETE /api/secured/v1/distributions/{user_id}/delete/{id}
- DELETE /api/secured/v1/distributions/{user_id}/{id}
- DELETE /api/secured/v1/distributions/{user_id}/stop_delete/{id}
- POST /api/secured/v1/stones/delete
- POST /api/frontend/v1/stones/purchase-status/{status}
- POST /api/secured/v1/stones/publish/{case}
- GET /api/frontend/v1/user/logout/info
- GET /api/secured/v1/user/logout

### API methods deprecated (will be removed in Cutwise v.4.0)

- GET /api/frontend/v1/profiles/{id}
- GET /api/secured/v1/profiles/{id}
- PUT /api/secured/v1/profiles/{id}
- GET /share/{product_type}/{cid} (use GET /share/{cid} instead!)
- GET /api/frontend/v1/stones
- GET /api/frontend/v1/stones/edit/{cid}
- POST /api/frontend/v1/stones/edit/{cid}
- GET /api/frontend/v1/stones_listing
- GET /api/frontend/v1/stonesbyids

### API properties

- Property isDistributionDeleted removed from /api/frontend/v1/stones/{cid} data
- Property isExView removed from /api/frontend/v1/stones/{cid} data

### CLI

- Command catalog-bundle:cron-delete-distributions is removed

### DB table removals

- agency_stone_page_contacts
- external_black_list
- external_codes
- external_users_devices
- external_stone_list
- external_view_stats
- external_view_list
- external_quotes
- external_users
- agency_stone_pages

### API methods added

- GET /api/v2/filters # filters with identifiers for correct clients work with Cutwise API v2
- FULL REST: /api/v2/media
- FULL REST: /api/v2/mediasubformats
- FULL REST: /api/v2/searchlists
- FULL REST: /api/v2/usercontacts # Functionality displacing external users
- FULL REST: /api/v2/setuppresets
- FULL REST: /api/v2/users
- GET/PUT/DELETE: /api/v2/searchlists/{searchListId}/products/{productId} # Managing Product state in SearchList
- POST /api/v2/sharing/bulk # Posting bulk sharing operation (BC: vendor sharing product for his contacts)

### API properties

- MediaSourceType identifiers in all requests

### DB tables added

- search_lists
- search_lists_products

## 2.9.0

- Moved to FOSRestBundle Context from JMS SerializeContenx
- Set max depth = 6 to all API request
