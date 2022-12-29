# Lenster API (Core) parsed (2022-12-27)

# Base URL : <https://api-mumbai.lens.dev/>

## 1) DefaultProfile

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

---

Req

---

Method: `POST`

Body:

---

```json
{
    "operationName": "DefaultProfile",
    "query": "query DefaultProfile {\n  defaultProfile(\n    request: {ethereumAddress: \"0x19DAec00955fecf6a4AC7158E395389Ca669Fb95\"}\n  ) {\n    id\n    name\n    bio\n    isDefault\n    attributes {\n      displayType\n      traitType\n      key\n      value\n    }\n    followNftAddress\n    metadata\n    handle\n    picture {\n      ... on NftImage {\n        contractAddress\n        tokenId\n        uri\n        chainId\n        verified\n      }\n      ... on MediaSet {\n        original {\n          url\n          mimeType\n        }\n      }\n    }\n    coverPicture {\n      ... on NftImage {\n        contractAddress\n        tokenId\n        uri\n        chainId\n        verified\n      }\n      ... on MediaSet {\n        original {\n          url\n          mimeType\n        }\n      }\n    }\n    ownedBy\n    dispatcher {\n      address\n      canUseRelay\n    }\n    stats {\n      totalFollowers\n      totalFollowing\n      totalPosts\n      totalComments\n      totalMirrors\n      totalPublications\n      totalCollects\n    }\n    followModule {\n      ... on FeeFollowModuleSettings {\n        type\n        contractAddress\n        amount {\n          asset {\n            name\n            symbol\n            decimals\n            address\n          }\n          value\n        }\n        recipient\n      }\n      ... on ProfileFollowModuleSettings {\n        type\n      }\n      ... on RevertFollowModuleSettings {\n        type\n      }\n    }\n  }\n}\n",    
    "variables": {}
}
```

---

Resp

---

```json
{
    "data": {
        "defaultProfile": null
    }
}
```

## 2) UserProfiles

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxNzkxMTksImV4cCI6MTY3MjE4MDkxOX0.8ILSstxGD8HM7aj87Va-U-ALxdn7SlFg1GV1_5YJCis

---

Req

---

Method: `POST`

Body:

---

```json
{
    "operationName": "UserProfiles",
    "query": "query UserProfiles($ownedBy: [EthereumAddress!]) {\n  profiles(request: {ownedBy: $ownedBy}) {\n    items {\n      ...ProfileFields\n      interests\n      stats {\n        totalFollowing\n        __typename\n      }\n      isDefault\n      dispatcher {\n        canUseRelay\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n  userSigNonces {\n    lensHubOnChainSigNonce\n    __typename\n  }\n}\n\nfragment ProfileFields on Profile {\n  id\n  name\n  handle\n  bio\n  ownedBy\n  isFollowedByMe\n  stats {\n    totalFollowers\n    totalFollowing\n    __typename\n  }\n  attributes {\n    key\n    value\n    __typename\n  }\n  picture {\n    ... on MediaSet {\n      original {\n        url\n        __typename\n      }\n      __typename\n    }\n    ... on NftImage {\n      uri\n      __typename\n    }\n    __typename\n  }\n  followModule {\n    __typename\n  }\n  __typename\n}",
    "variables": {"ownedBy": "0x19DAec00955fecf6a4AC7158E395389Ca669Fb95"}
}
```

---

Resp

---

```json
{
    "data": {
        "profiles": {
            "items": [],
            "__typename": "PaginatedProfileResult"
        },
        "userSigNonces": {
            "lensHubOnChainSigNonce": 0,
            "__typename": "UserSigNonces"
        }
    }
}
```

## 3) Login

    (1/2 Challenge)

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "operationName": "Challenge",
    "query": "query Challenge {\n  challenge(request: {address: \"0x19DAec00955fecf6a4AC7158E395389Ca669Fb95\"}) {\n    text\n  }\n}\n",
    "variables": {}
}
```

---

Resp

---

```json
{
    "data": {
        "challenge": {
            "text": "\nunknown wants you to sign in with your Ethereum account:\n0x19DAec00955fecf6a4AC7158E395389Ca669Fb95\n\nSign in with ethereum to lens\n\nURI: unknown\nVersion: 1\nChain ID: 80001\nNonce: 29c4f1e428be82f3\nIssued At: 2022-12-28T01:39:47.497Z\n "
        }
    }
}
```

    (2/2 Authenticate)

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

---

Req

---

Method: `POST`

Body:

---

```json
{
    "operationName": "Authenticate",
    "query": "mutation Authenticate($request: SignedAuthChallenge!) {\n  authenticate(request: $request) {\n    accessToken\n    refreshToken\n    __typename\n  }\n}",
    "variables": {
        "request": {
            "address": "0x19DAec00955fecf6a4AC7158E395389Ca669Fb95",
            "signature": "0x9e19113a44a36570535d71e9807f75c1ebfdd4dd25934060d57f07fa54b9aa657680a2ee84bdcd96b3c9d336689928f2e7a48d2c8971a59a0642f60d06fb4bbd1b"
        }
    }
}
```

---

Resp

---

```json
{
    "data": {
        "authenticate": {
            "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTQwOTYsImV4cCI6MTY3MjE5NTg5Nn0.1bpjuPMjGH7vXN1PLrRAT3tVWJt4ClsCf94Trss6fp8",
            "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJyZWZyZXNoIiwiaWF0IjoxNjcyMTk0MDk2LCJleHAiOjE2NzI3OTg4OTZ9.q7-UrBog6oug-UXP1H4NjJIuDqY80lmmsRtTvaPD-Vw",
            "__typename": "AuthenticationResult"
        }
    }
}
```

## 4) CreateProfile

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTUxNTMsImV4cCI6MTY3MjE5Njk1M30.3pqY5eBxRleP1B8yP6hxY41jHt8SbXO_LZJjB6FsSNQ

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "operationName": "CreateProfile",
    "query": "mutation CreateProfile {\n  createProfile(\n    request: {handle: \"davfromsecret\", profilePictureUri: \"https://storage.googleapis.com/opensea-prod.appspot.com/puffs/3.png\", followNFTURI: null, followModule: {freeFollowModule: true}}\n  ) {\n    ... on RelayerResult {\n      txHash\n    }\n    ... on RelayError {\n      reason\n    }\n    __typename\n  }\n}\n",
    "variables":{}
}
```

---

Resp

---

```json
{
    "data": {
        "createProfile": {
            "txHash": "0xca56814e4017704eaa31bbf1d9c9d119a805d6e1e7fac9f1566ede87aa2349f4",
            "__typename": "RelayerResult"
        }
    }
}
```

## 5) Comment

    (1/2 CreateCommentTypedData)

Heade
---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTUxNTMsImV4cCI6MTY3MjE5Njk1M30.3pqY5eBxRleP1B8yP6hxY41jHt8SbXO_LZJjB6FsSNQ

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "operationName": "CreateCommentTypedData",
    "query": "mutation CreateCommentTypedData($options: TypedDataOptions, $request: CreatePublicCommentRequest!) {\n  createCommentTypedData(options: $options, request: $request) {\n    id\n    expiresAt\n    typedData {\n      types {\n        CommentWithSig {\n          name\n          type\n          __typename\n        }\n        __typename\n      }\n      domain {\n        name\n        chainId\n        version\n        verifyingContract\n        __typename\n      }\n      value {\n        nonce\n        deadline\n        profileId\n        profileIdPointed\n        pubIdPointed\n        contentURI\n        collectModule\n        collectModuleInitData\n        referenceModule\n        referenceModuleData\n        referenceModuleInitData\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}",
    "variables": {
        "options": {
            "overrideSigNonce": 1
        },
        "request": {
            "profileId": "0x5fc0",
            "contentURI": "https://arweave.net/Cc668jE3Ylsg98LF_-4QpMEZIAwoqI55Cs8oASQ9iE8",
            "publicationId": "0x1b-0x0118",
            "collectModule": {
                "revertCollectModule": true
            },
            "referenceModule": {
                "followerOnlyReferenceModule": false
            }
        }
    }
}
```

---

Resp

---

```json
{
    "data": {
        "createCommentTypedData": {
            "id": "b87b33db-3eca-405f-8da4-2dda2609858b",
            "expiresAt": "2022-12-28T03:49:15.000Z",
            "typedData": {
                "types": {
                    "CommentWithSig": [
                        {
                            "name": "profileId",
                            "type": "uint256",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "contentURI",
                            "type": "string",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "profileIdPointed",
                            "type": "uint256",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "pubIdPointed",
                            "type": "uint256",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "referenceModuleData",
                            "type": "bytes",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "collectModule",
                            "type": "address",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "collectModuleInitData",
                            "type": "bytes",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "referenceModule",
                            "type": "address",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "referenceModuleInitData",
                            "type": "bytes",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "nonce",
                            "type": "uint256",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "deadline",
                            "type": "uint256",
                            "__typename": "EIP712TypedDataField"
                        }
                    ],
                    "__typename": "CreateCommentEIP712TypedDataTypes"
                },
                "domain": {
                    "name": "Lens Protocol Profiles",
                    "chainId": 80001,
                    "version": "1",
                    "verifyingContract": "0x60Ae865ee4C725cd04353b5AAb364553f56ceF82",
                    "__typename": "EIP712TypedDataDomain"
                },
                "value": {
                    "nonce": 1,
                    "deadline": 1672199355,
                    "profileId": "0x5fc0",
                    "profileIdPointed": "0x1b",
                    "pubIdPointed": "0x0118",
                    "contentURI": "https://arweave.net/Cc668jE3Ylsg98LF_-4QpMEZIAwoqI55Cs8oASQ9iE8",
                    "collectModule": "0x5E70fFD2C6D04d65C3abeBa64E93082cfA348dF8",
                    "collectModuleInitData": "0x",
                    "referenceModule": "0x0000000000000000000000000000000000000000",
                    "referenceModuleData": "0x",
                    "referenceModuleInitData": "0x",
                    "__typename": "CreateCommentEIP712TypedDataValue"
                },
                "__typename": "CreateCommentEIP712TypedData"
            },
            "__typename": "CreateCommentBroadcastItemResult"
        }
    }
}
```

---

    (2/2 CommentFeed)

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTUxNTMsImV4cCI6MTY3MjE5Njk1M30.3pqY5eBxRleP1B8yP6hxY41jHt8SbXO_LZJjB6FsSNQ

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "operationName": "CommentFeed",
    "variables": {
        "request": {
            "commentsOf": "0x1b-0x0118",
            "customFilters": [
                "GARDENERS"
            ],
            "limit": 10
        },
        "reactionRequest": {
            "profileId": "0x5fc0"
        },
        "profileId": "0x5fc0"
    },
    "query": "query CommentFeed($request: PublicationsQueryRequest!, $reactionRequest: ReactionFieldResolverRequest, $profileId: ProfileId) {\n  publications(request: $request) {\n    items {\n      ... on Comment {\n        ...CommentFields\n        __typename\n      }\n      __typename\n    }\n    pageInfo {\n      totalCount\n      next\n      __typename\n    }\n    __typename\n  }\n}\n\nfragment CommentFields on Comment {\n  id\n  profile {\n    ...ProfileFields\n    __typename\n  }\n  reaction(request: $reactionRequest)\n  mirrors(by: $profileId)\n  hasCollectedByMe\n  onChainContentURI\n  canComment(profileId: $profileId) {\n    result\n    __typename\n  }\n  canMirror(profileId: $profileId) {\n    result\n    __typename\n  }\n  canDecrypt(profileId: $profileId) {\n    result\n    reasons\n    __typename\n  }\n  collectedBy {\n    address\n    defaultProfile {\n      ...ProfileFields\n      __typename\n    }\n    __typename\n  }\n  collectModule {\n    ...CollectModuleFields\n    __typename\n  }\n  stats {\n    ...StatsFields\n    __typename\n  }\n  metadata {\n    ...MetadataFields\n    __typename\n  }\n  hidden\n  createdAt\n  appId\n  commentOn {\n    ... on Post {\n      ...PostFields\n      __typename\n    }\n    ... on Comment {\n      id\n      profile {\n        ...ProfileFields\n        __typename\n      }\n      reaction(request: $reactionRequest)\n      mirrors(by: $profileId)\n      hasCollectedByMe\n      onChainContentURI\n      canComment(profileId: $profileId) {\n        result\n        __typename\n      }\n      canMirror(profileId: $profileId) {\n        result\n        __typename\n      }\n      canDecrypt(profileId: $profileId) {\n        result\n        reasons\n        __typename\n      }\n      collectedBy {\n        address\n        defaultProfile {\n          handle\n          __typename\n        }\n        __typename\n      }\n      collectModule {\n        ...CollectModuleFields\n        __typename\n      }\n      metadata {\n        ...MetadataFields\n        __typename\n      }\n      stats {\n        ...StatsFields\n        __typename\n      }\n      mainPost {\n        ... on Post {\n          ...PostFields\n          __typename\n        }\n        ... on Mirror {\n          ...MirrorFields\n          __typename\n        }\n        __typename\n      }\n      hidden\n      createdAt\n      __typename\n    }\n    ... on Mirror {\n      ...MirrorFields\n      __typename\n    }\n    __typename\n  }\n  __typename\n}\n\nfragment ProfileFields on Profile {\n  id\n  name\n  handle\n  bio\n  ownedBy\n  isFollowedByMe\n  stats {\n    totalFollowers\n    totalFollowing\n    __typename\n  }\n  attributes {\n    key\n    value\n    __typename\n  }\n  picture {\n    ... on MediaSet {\n      original {\n        url\n        __typename\n      }\n      __typename\n    }\n    ... on NftImage {\n      uri\n      __typename\n    }\n    __typename\n  }\n  followModule {\n    __typename\n  }\n  __typename\n}\n\nfragment CollectModuleFields on CollectModule {\n  ... on FreeCollectModuleSettings {\n    type\n    contractAddress\n    followerOnly\n    __typename\n  }\n  ... on FeeCollectModuleSettings {\n    type\n    referralFee\n    contractAddress\n    followerOnly\n    amount {\n      asset {\n        symbol\n        decimals\n        address\n        __typename\n      }\n      value\n      __typename\n    }\n    __typename\n  }\n  ... on LimitedFeeCollectModuleSettings {\n    type\n    collectLimit\n    referralFee\n    contractAddress\n    followerOnly\n    amount {\n      asset {\n        symbol\n        decimals\n        address\n        __typename\n      }\n      value\n      __typename\n    }\n    __typename\n  }\n  ... on LimitedTimedFeeCollectModuleSettings {\n    type\n    collectLimit\n    endTimestamp\n    referralFee\n    contractAddress\n    followerOnly\n    amount {\n      asset {\n        symbol\n        decimals\n        address\n        __typename\n      }\n      value\n      __typename\n    }\n    __typename\n  }\n  ... on TimedFeeCollectModuleSettings {\n    type\n    endTimestamp\n    referralFee\n    contractAddress\n    followerOnly\n    amount {\n      asset {\n        symbol\n        decimals\n        address\n        __typename\n      }\n      value\n      __typename\n    }\n    __typename\n  }\n  __typename\n}\n\nfragment StatsFields on PublicationStats {\n  totalUpvotes\n  totalAmountOfMirrors\n  totalAmountOfCollects\n  totalAmountOfComments\n  __typename\n}\n\nfragment MetadataFields on MetadataOutput {\n  name\n  description\n  content\n  image\n  attributes {\n    traitType\n    value\n    __typename\n  }\n  cover {\n    original {\n      url\n      __typename\n    }\n    __typename\n  }\n  media {\n    original {\n      url\n      mimeType\n      __typename\n    }\n    __typename\n  }\n  encryptionParams {\n    accessCondition {\n      or {\n        criteria {\n          ...SimpleConditionFields\n          and {\n            criteria {\n              ...SimpleConditionFields\n              __typename\n            }\n            __typename\n          }\n          or {\n            criteria {\n              ...SimpleConditionFields\n              __typename\n            }\n            __typename\n          }\n          __typename\n        }\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n  __typename\n}\n\nfragment SimpleConditionFields on AccessConditionOutput {\n  nft {\n    contractAddress\n    chainID\n    contractType\n    tokenIds\n    __typename\n  }\n  eoa {\n    address\n    __typename\n  }\n  token {\n    contractAddress\n    amount\n    chainID\n    condition\n    decimals\n    __typename\n  }\n  follow {\n    profileId\n    __typename\n  }\n  collect {\n    publicationId\n    thisPublication\n    __typename\n  }\n  __typename\n}\n\nfragment PostFields on Post {\n  id\n  profile {\n    ...ProfileFields\n    __typename\n  }\n  reaction(request: $reactionRequest)\n  mirrors(by: $profileId)\n  hasCollectedByMe\n  onChainContentURI\n  canComment(profileId: $profileId) {\n    result\n    __typename\n  }\n  canMirror(profileId: $profileId) {\n    result\n    __typename\n  }\n  canDecrypt(profileId: $profileId) {\n    result\n    reasons\n    __typename\n  }\n  collectedBy {\n    address\n    defaultProfile {\n      ...ProfileFields\n      __typename\n    }\n    __typename\n  }\n  collectModule {\n    ...CollectModuleFields\n    __typename\n  }\n  stats {\n    ...StatsFields\n    __typename\n  }\n  metadata {\n    ...MetadataFields\n    __typename\n  }\n  hidden\n  createdAt\n  appId\n  __typename\n}\n\nfragment MirrorFields on Mirror {\n  id\n  profile {\n    ...ProfileFields\n    __typename\n  }\n  reaction(request: $reactionRequest)\n  canComment(profileId: $profileId) {\n    result\n    __typename\n  }\n  canMirror(profileId: $profileId) {\n    result\n    __typename\n  }\n  canDecrypt(profileId: $profileId) {\n    result\n    reasons\n    __typename\n  }\n  collectModule {\n    ...CollectModuleFields\n    __typename\n  }\n  stats {\n    ...StatsFields\n    __typename\n  }\n  metadata {\n    ...MetadataFields\n    __typename\n  }\n  hidden\n  mirrorOf {\n    ... on Post {\n      ...PostFields\n      __typename\n    }\n    ... on Comment {\n      id\n      profile {\n        ...ProfileFields\n        __typename\n      }\n      reaction(request: $reactionRequest)\n      mirrors(by: $profileId)\n      onChainContentURI\n      canComment(profileId: $profileId) {\n        result\n        __typename\n      }\n      canMirror(profileId: $profileId) {\n        result\n        __typename\n      }\n      canDecrypt(profileId: $profileId) {\n        result\n        reasons\n        __typename\n      }\n      stats {\n        ...StatsFields\n        __typename\n      }\n      createdAt\n      __typename\n    }\n    __typename\n  }\n  createdAt\n  appId\n  __typename\n}"
}
```

---

Resp

---

```json
{
    "data": {
        "publications": {
            "items": [
                {
                    "id": "0x5fc0-0x02",
                    "profile": {
                        "id": "0x5fc0",
                        "name": null,
                        "handle": "davfromsecret.test",
                        "bio": null,
                        "ownedBy": "0x19DAec00955fecf6a4AC7158E395389Ca669Fb95",
                        "isFollowedByMe": false,
                        "stats": {
                            "totalFollowers": 0,
                            "totalFollowing": 0,
                            "__typename": "ProfileStats"
                        },
                        "attributes": [],
                        "picture": {
                            "original": {
                                "url": "https://storage.googleapis.com/opensea-prod.appspot.com/puffs/3.png",
                                "__typename": "Media"
                            },
                            "__typename": "MediaSet"
                        },
                        "followModule": null,
                        "__typename": "Profile"
                    },
                    "reaction": null,
                    "mirrors": [],
                    "hasCollectedByMe": false,
                    "onChainContentURI": "https://arweave.net/Cc668jE3Ylsg98LF_-4QpMEZIAwoqI55Cs8oASQ9iE8",
                    "canComment": {
                        "result": true,
                        "__typename": "CanCommentResponse"
                    },
                    "canMirror": {
                        "result": true,
                        "__typename": "CanMirrorResponse"
                    },
                    "canDecrypt": {
                        "result": false,
                        "reasons": [
                            "MISSING_ENCRYPTION_PARAMS"
                        ],
                        "__typename": "CanDecryptResponse"
                    },
                    "collectedBy": null,
                    "collectModule": {
                        "__typename": "RevertCollectModuleSettings"
                    },
                    "stats": {
                        "totalUpvotes": 0,
                        "totalAmountOfMirrors": 0,
                        "totalAmountOfCollects": 0,
                        "totalAmountOfComments": 0,
                        "__typename": "PublicationStats"
                    },
                    "metadata": {
                        "name": "Comment by @davfromsecret.test",
                        "description": "hoho",
                        "content": "hoho",
                        "image": null,
                        "attributes": [
                            {
                                "traitType": "type",
                                "value": "text_only",
                                "__typename": "MetadataAttributeOutput"
                            }
                        ],
                        "cover": null,
                        "media": [],
                        "encryptionParams": null,
                        "__typename": "MetadataOutput"
                    },
                    "hidden": false,
                    "createdAt": "2022-12-28T03:46:47.000Z",
                    "appId": "lenster",
                    "commentOn": {
                        "id": "0x1b-0x0118",
                        "profile": {
                            "id": "0x1b",
                            "name": null,
                            "handle": "brainjammer.test",
                            "bio": null,
                            "ownedBy": "0x248ba21F6ff51cf0CD4765C3Bc9fAD2030a591d5",
                            "isFollowedByMe": false,
                            "stats": {
                                "totalFollowers": 33,
                                "totalFollowing": 28,
                                "__typename": "ProfileStats"
                            },
                            "attributes": [],
                            "picture": {
                                "original": {
                                    "url": "https://statics-mumbai-lens-staging.s3.eu-west-1.amazonaws.com/profile/QmVeEwimhwaebeHFDTVY3XNjFuaNUWuhv1ksNefnzeTKXH",
                                    "__typename": "Media"
                                },
                                "__typename": "MediaSet"
                            },
                            "followModule": {
                                "__typename": "FeeFollowModuleSettings"
                            },
                            "__typename": "Profile"
                        },
                        "reaction": null,
                        "mirrors": [],
                        "hasCollectedByMe": false,
                        "onChainContentURI": "https://arweave.net/q8imNDMKotHTRsVDGP2pS6Id-dpsG_YTIbg-0x9i3Yc",
                        "canComment": {
                            "result": true,
                            "__typename": "CanCommentResponse"
                        },
                        "canMirror": {
                            "result": true,
                            "__typename": "CanMirrorResponse"
                        },
                        "canDecrypt": {
                            "result": false,
                            "reasons": [
                                "MISSING_ENCRYPTION_PARAMS"
                            ],
                            "__typename": "CanDecryptResponse"
                        },
                        "collectedBy": null,
                        "collectModule": {
                            "__typename": "RevertCollectModuleSettings"
                        },
                        "stats": {
                            "totalUpvotes": 0,
                            "totalAmountOfMirrors": 1,
                            "totalAmountOfCollects": 0,
                            "totalAmountOfComments": 5,
                            "__typename": "PublicationStats"
                        },
                        "metadata": {
                            "name": "none",
                            "description": null,
                            "content": "This one will show in all my browser tabs",
                            "image": null,
                            "attributes": [],
                            "cover": null,
                            "media": [],
                            "encryptionParams": null,
                            "__typename": "MetadataOutput"
                        },
                        "hidden": false,
                        "createdAt": "2022-12-22T19:11:59.000Z",
                        "appId": null,
                        "__typename": "Post"
                    },
                    "__typename": "Comment"
                },
                {
                    "id": "0x5fc0-0x01",
                    "profile": {
                        "id": "0x5fc0",
                        "name": null,
                        "handle": "davfromsecret.test",
                        "bio": null,
                        "ownedBy": "0x19DAec00955fecf6a4AC7158E395389Ca669Fb95",
                        "isFollowedByMe": false,
                        "stats": {
                            "totalFollowers": 0,
                            "totalFollowing": 0,
                            "__typename": "ProfileStats"
                        },
                        "attributes": [],
                        "picture": {
                            "original": {
                                "url": "https://storage.googleapis.com/opensea-prod.appspot.com/puffs/3.png",
                                "__typename": "Media"
                            },
                            "__typename": "MediaSet"
                        },
                        "followModule": null,
                        "__typename": "Profile"
                    },
                    "reaction": null,
                    "mirrors": [],
                    "hasCollectedByMe": false,
                    "onChainContentURI": "https://arweave.net/9qo_yzbhh4ynQQbvAAKBD89g2zETMr_PxIFoWRrks40",
                    "canComment": {
                        "result": true,
                        "__typename": "CanCommentResponse"
                    },
                    "canMirror": {
                        "result": true,
                        "__typename": "CanMirrorResponse"
                    },
                    "canDecrypt": {
                        "result": false,
                        "reasons": [
                            "MISSING_ENCRYPTION_PARAMS"
                        ],
                        "__typename": "CanDecryptResponse"
                    },
                    "collectedBy": null,
                    "collectModule": {
                        "__typename": "RevertCollectModuleSettings"
                    },
                    "stats": {
                        "totalUpvotes": 0,
                        "totalAmountOfMirrors": 0,
                        "totalAmountOfCollects": 0,
                        "totalAmountOfComments": 0,
                        "__typename": "PublicationStats"
                    },
                    "metadata": {
                        "name": "Comment by @davfromsecret.test",
                        "description": "haha",
                        "content": "haha",
                        "image": null,
                        "attributes": [
                            {
                                "traitType": "type",
                                "value": "text_only",
                                "__typename": "MetadataAttributeOutput"
                            }
                        ],
                        "cover": null,
                        "media": [],
                        "encryptionParams": null,
                        "__typename": "MetadataOutput"
                    },
                    "hidden": false,
                    "createdAt": "2022-12-28T03:11:03.000Z",
                    "appId": "lenster",
                    "commentOn": {
                        "id": "0x1b-0x0118",
                        "profile": {
                            "id": "0x1b",
                            "name": null,
                            "handle": "brainjammer.test",
                            "bio": null,
                            "ownedBy": "0x248ba21F6ff51cf0CD4765C3Bc9fAD2030a591d5",
                            "isFollowedByMe": false,
                            "stats": {
                                "totalFollowers": 33,
                                "totalFollowing": 28,
                                "__typename": "ProfileStats"
                            },
                            "attributes": [],
                            "picture": {
                                "original": {
                                    "url": "https://statics-mumbai-lens-staging.s3.eu-west-1.amazonaws.com/profile/QmVeEwimhwaebeHFDTVY3XNjFuaNUWuhv1ksNefnzeTKXH",
                                    "__typename": "Media"
                                },
                                "__typename": "MediaSet"
                            },
                            "followModule": {
                                "__typename": "FeeFollowModuleSettings"
                            },
                            "__typename": "Profile"
                        },
                        "reaction": null,
                        "mirrors": [],
                        "hasCollectedByMe": false,
                        "onChainContentURI": "https://arweave.net/q8imNDMKotHTRsVDGP2pS6Id-dpsG_YTIbg-0x9i3Yc",
                        "canComment": {
                            "result": true,
                            "__typename": "CanCommentResponse"
                        },
                        "canMirror": {
                            "result": true,
                            "__typename": "CanMirrorResponse"
                        },
                        "canDecrypt": {
                            "result": false,
                            "reasons": [
                                "MISSING_ENCRYPTION_PARAMS"
                            ],
                            "__typename": "CanDecryptResponse"
                        },
                        "collectedBy": null,
                        "collectModule": {
                            "__typename": "RevertCollectModuleSettings"
                        },
                        "stats": {
                            "totalUpvotes": 0,
                            "totalAmountOfMirrors": 1,
                            "totalAmountOfCollects": 0,
                            "totalAmountOfComments": 5,
                            "__typename": "PublicationStats"
                        },
                        "metadata": {
                            "name": "none",
                            "description": null,
                            "content": "This one will show in all my browser tabs",
                            "image": null,
                            "attributes": [],
                            "cover": null,
                            "media": [],
                            "encryptionParams": null,
                            "__typename": "MetadataOutput"
                        },
                        "hidden": false,
                        "createdAt": "2022-12-22T19:11:59.000Z",
                        "appId": null,
                        "__typename": "Post"
                    },
                    "__typename": "Comment"
                },
                {
                    "id": "0x4ca3-0x04",
                    "profile": {
                        "id": "0x4ca3",
                        "name": null,
                        "handle": "satwikmj.test",
                        "bio": null,
                        "ownedBy": "0x7A1889B74A891D621C91DA63D7CE25140D6FaA20",
                        "isFollowedByMe": false,
                        "stats": {
                            "totalFollowers": 2,
                            "totalFollowing": 98,
                            "__typename": "ProfileStats"
                        },
                        "attributes": [],
                        "picture": {
                            "original": {
                                "url": "https://ipfs.io/ipfs/QmPpX9KyuPyWv2ayTDv3ETterWdNtZWKujoJrBqvo5KqV2",
                                "__typename": "Media"
                            },
                            "__typename": "MediaSet"
                        },
                        "followModule": null,
                        "__typename": "Profile"
                    },
                    "reaction": null,
                    "mirrors": [],
                    "hasCollectedByMe": false,
                    "onChainContentURI": "https://arweave.net/cH5JBl0Y2TsaW_lXbJnD91iL9JKaJab8sXxFTyId5UI",
                    "canComment": {
                        "result": false,
                        "__typename": "CanCommentResponse"
                    },
                    "canMirror": {
                        "result": false,
                        "__typename": "CanMirrorResponse"
                    },
                    "canDecrypt": {
                        "result": false,
                        "reasons": [
                            "MISSING_ENCRYPTION_PARAMS"
                        ],
                        "__typename": "CanDecryptResponse"
                    },
                    "collectedBy": null,
                    "collectModule": {
                        "__typename": "RevertCollectModuleSettings"
                    },
                    "stats": {
                        "totalUpvotes": 0,
                        "totalAmountOfMirrors": 0,
                        "totalAmountOfCollects": 0,
                        "totalAmountOfComments": 0,
                        "__typename": "PublicationStats"
                    },
                    "metadata": {
                        "name": "Comment by @satwikmj.test",
                        "description": "ok",
                        "content": "ok",
                        "image": null,
                        "attributes": [
                            {
                                "traitType": "type",
                                "value": "text_only",
                                "__typename": "MetadataAttributeOutput"
                            }
                        ],
                        "cover": null,
                        "media": [],
                        "encryptionParams": null,
                        "__typename": "MetadataOutput"
                    },
                    "hidden": false,
                    "createdAt": "2022-12-26T09:59:44.000Z",
                    "appId": "lenster",
                    "commentOn": {
                        "id": "0x1b-0x0118",
                        "profile": {
                            "id": "0x1b",
                            "name": null,
                            "handle": "brainjammer.test",
                            "bio": null,
                            "ownedBy": "0x248ba21F6ff51cf0CD4765C3Bc9fAD2030a591d5",
                            "isFollowedByMe": false,
                            "stats": {
                                "totalFollowers": 33,
                                "totalFollowing": 28,
                                "__typename": "ProfileStats"
                            },
                            "attributes": [],
                            "picture": {
                                "original": {
                                    "url": "https://statics-mumbai-lens-staging.s3.eu-west-1.amazonaws.com/profile/QmVeEwimhwaebeHFDTVY3XNjFuaNUWuhv1ksNefnzeTKXH",
                                    "__typename": "Media"
                                },
                                "__typename": "MediaSet"
                            },
                            "followModule": {
                                "__typename": "FeeFollowModuleSettings"
                            },
                            "__typename": "Profile"
                        },
                        "reaction": null,
                        "mirrors": [],
                        "hasCollectedByMe": false,
                        "onChainContentURI": "https://arweave.net/q8imNDMKotHTRsVDGP2pS6Id-dpsG_YTIbg-0x9i3Yc",
                        "canComment": {
                            "result": true,
                            "__typename": "CanCommentResponse"
                        },
                        "canMirror": {
                            "result": true,
                            "__typename": "CanMirrorResponse"
                        },
                        "canDecrypt": {
                            "result": false,
                            "reasons": [
                                "MISSING_ENCRYPTION_PARAMS"
                            ],
                            "__typename": "CanDecryptResponse"
                        },
                        "collectedBy": null,
                        "collectModule": {
                            "__typename": "RevertCollectModuleSettings"
                        },
                        "stats": {
                            "totalUpvotes": 0,
                            "totalAmountOfMirrors": 1,
                            "totalAmountOfCollects": 0,
                            "totalAmountOfComments": 5,
                            "__typename": "PublicationStats"
                        },
                        "metadata": {
                            "name": "none",
                            "description": null,
                            "content": "This one will show in all my browser tabs",
                            "image": null,
                            "attributes": [],
                            "cover": null,
                            "media": [],
                            "encryptionParams": null,
                            "__typename": "MetadataOutput"
                        },
                        "hidden": false,
                        "createdAt": "2022-12-22T19:11:59.000Z",
                        "appId": null,
                        "__typename": "Post"
                    },
                    "__typename": "Comment"
                },
                {
                    "id": "0x15-0x0263",
                    "profile": {
                        "id": "0x15",
                        "name": "Yoginth",
                        "handle": "yoginth.test",
                        "bio": "Test",
                        "ownedBy": "0x3A5bd1E37b099aE3386D13947b6a90d97675e5e3",
                        "isFollowedByMe": false,
                        "stats": {
                            "totalFollowers": 268,
                            "totalFollowing": 58,
                            "__typename": "ProfileStats"
                        },
                        "attributes": [
                            {
                                "key": "location",
                                "value": "India",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "twitter",
                                "value": "yogicodes",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "hasPrideLogo",
                                "value": "true",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "app",
                                "value": "Lenster",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "app_name",
                                "value": "wagmifund",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "cardView",
                                "value": "card",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "corners",
                                "value": "0.9",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "gradient",
                                "value": "true",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "theme",
                                "value": "{\"h\":159,\"s\":0.94,\"l\":0.43,\"a\":1}",
                                "__typename": "Attribute"
                            }
                        ],
                        "picture": {
                            "original": {
                                "url": "https://lens.infura-ipfs.io/ipfs/Qma8mXoeorvPqodDazf7xqARoFD394s1njkze7q1X4CK8U",
                                "__typename": "Media"
                            },
                            "__typename": "MediaSet"
                        },
                        "followModule": null,
                        "__typename": "Profile"
                    },
                    "reaction": null,
                    "mirrors": [],
                    "hasCollectedByMe": false,
                    "onChainContentURI": "https://arweave.net/ky4oHJWh52pFFrq-Sob91FZgYcovEeAprGzy8FSAQEM",
                    "canComment": {
                        "result": false,
                        "__typename": "CanCommentResponse"
                    },
                    "canMirror": {
                        "result": false,
                        "__typename": "CanMirrorResponse"
                    },
                    "canDecrypt": {
                        "result": false,
                        "reasons": [
                            "MISSING_ENCRYPTION_PARAMS"
                        ],
                        "__typename": "CanDecryptResponse"
                    },
                    "collectedBy": null,
                    "collectModule": {
                        "__typename": "RevertCollectModuleSettings"
                    },
                    "stats": {
                        "totalUpvotes": 0,
                        "totalAmountOfMirrors": 0,
                        "totalAmountOfCollects": 0,
                        "totalAmountOfComments": 0,
                        "__typename": "PublicationStats"
                    },
                    "metadata": {
                        "name": "Comment by @yoginth.test",
                        "description": "gm",
                        "content": "gm",
                        "image": null,
                        "attributes": [
                            {
                                "traitType": "type",
                                "value": "text_only",
                                "__typename": "MetadataAttributeOutput"
                            }
                        ],
                        "cover": null,
                        "media": [],
                        "encryptionParams": null,
                        "__typename": "MetadataOutput"
                    },
                    "hidden": false,
                    "createdAt": "2022-12-25T05:02:41.000Z",
                    "appId": "lenster",
                    "commentOn": {
                        "id": "0x1b-0x0118",
                        "profile": {
                            "id": "0x1b",
                            "name": null,
                            "handle": "brainjammer.test",
                            "bio": null,
                            "ownedBy": "0x248ba21F6ff51cf0CD4765C3Bc9fAD2030a591d5",
                            "isFollowedByMe": false,
                            "stats": {
                                "totalFollowers": 33,
                                "totalFollowing": 28,
                                "__typename": "ProfileStats"
                            },
                            "attributes": [],
                            "picture": {
                                "original": {
                                    "url": "https://statics-mumbai-lens-staging.s3.eu-west-1.amazonaws.com/profile/QmVeEwimhwaebeHFDTVY3XNjFuaNUWuhv1ksNefnzeTKXH",
                                    "__typename": "Media"
                                },
                                "__typename": "MediaSet"
                            },
                            "followModule": {
                                "__typename": "FeeFollowModuleSettings"
                            },
                            "__typename": "Profile"
                        },
                        "reaction": null,
                        "mirrors": [],
                        "hasCollectedByMe": false,
                        "onChainContentURI": "https://arweave.net/q8imNDMKotHTRsVDGP2pS6Id-dpsG_YTIbg-0x9i3Yc",
                        "canComment": {
                            "result": true,
                            "__typename": "CanCommentResponse"
                        },
                        "canMirror": {
                            "result": true,
                            "__typename": "CanMirrorResponse"
                        },
                        "canDecrypt": {
                            "result": false,
                            "reasons": [
                                "MISSING_ENCRYPTION_PARAMS"
                            ],
                            "__typename": "CanDecryptResponse"
                        },
                        "collectedBy": null,
                        "collectModule": {
                            "__typename": "RevertCollectModuleSettings"
                        },
                        "stats": {
                            "totalUpvotes": 0,
                            "totalAmountOfMirrors": 1,
                            "totalAmountOfCollects": 0,
                            "totalAmountOfComments": 5,
                            "__typename": "PublicationStats"
                        },
                        "metadata": {
                            "name": "none",
                            "description": null,
                            "content": "This one will show in all my browser tabs",
                            "image": null,
                            "attributes": [],
                            "cover": null,
                            "media": [],
                            "encryptionParams": null,
                            "__typename": "MetadataOutput"
                        },
                        "hidden": false,
                        "createdAt": "2022-12-22T19:11:59.000Z",
                        "appId": null,
                        "__typename": "Post"
                    },
                    "__typename": "Comment"
                },
                {
                    "id": "0x15-0x0262",
                    "profile": {
                        "id": "0x15",
                        "name": "Yoginth",
                        "handle": "yoginth.test",
                        "bio": "Test",
                        "ownedBy": "0x3A5bd1E37b099aE3386D13947b6a90d97675e5e3",
                        "isFollowedByMe": false,
                        "stats": {
                            "totalFollowers": 268,
                            "totalFollowing": 58,
                            "__typename": "ProfileStats"
                        },
                        "attributes": [
                            {
                                "key": "location",
                                "value": "India",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "twitter",
                                "value": "yogicodes",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "hasPrideLogo",
                                "value": "true",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "app",
                                "value": "Lenster",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "app_name",
                                "value": "wagmifund",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "cardView",
                                "value": "card",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "corners",
                                "value": "0.9",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "gradient",
                                "value": "true",
                                "__typename": "Attribute"
                            },
                            {
                                "key": "theme",
                                "value": "{\"h\":159,\"s\":0.94,\"l\":0.43,\"a\":1}",
                                "__typename": "Attribute"
                            }
                        ],
                        "picture": {
                            "original": {
                                "url": "https://lens.infura-ipfs.io/ipfs/Qma8mXoeorvPqodDazf7xqARoFD394s1njkze7q1X4CK8U",
                                "__typename": "Media"
                            },
                            "__typename": "MediaSet"
                        },
                        "followModule": null,
                        "__typename": "Profile"
                    },
                    "reaction": null,
                    "mirrors": [],
                    "hasCollectedByMe": false,
                    "onChainContentURI": "https://arweave.net/BlYdNe1HNA5ZmMTEeJSmXRrAOpKaZu33TP5kAN2yPDE",
                    "canComment": {
                        "result": false,
                        "__typename": "CanCommentResponse"
                    },
                    "canMirror": {
                        "result": false,
                        "__typename": "CanMirrorResponse"
                    },
                    "canDecrypt": {
                        "result": false,
                        "reasons": [
                            "MISSING_ENCRYPTION_PARAMS"
                        ],
                        "__typename": "CanDecryptResponse"
                    },
                    "collectedBy": null,
                    "collectModule": {
                        "__typename": "RevertCollectModuleSettings"
                    },
                    "stats": {
                        "totalUpvotes": 0,
                        "totalAmountOfMirrors": 0,
                        "totalAmountOfCollects": 0,
                        "totalAmountOfComments": 0,
                        "__typename": "PublicationStats"
                    },
                    "metadata": {
                        "name": "Comment by @yoginth.test",
                        "description": "gm",
                        "content": "gm",
                        "image": null,
                        "attributes": [
                            {
                                "traitType": "type",
                                "value": "text_only",
                                "__typename": "MetadataAttributeOutput"
                            }
                        ],
                        "cover": null,
                        "media": [],
                        "encryptionParams": null,
                        "__typename": "MetadataOutput"
                    },
                    "hidden": false,
                    "createdAt": "2022-12-25T05:02:07.000Z",
                    "appId": "lenster",
                    "commentOn": {
                        "id": "0x1b-0x0118",
                        "profile": {
                            "id": "0x1b",
                            "name": null,
                            "handle": "brainjammer.test",
                            "bio": null,
                            "ownedBy": "0x248ba21F6ff51cf0CD4765C3Bc9fAD2030a591d5",
                            "isFollowedByMe": false,
                            "stats": {
                                "totalFollowers": 33,
                                "totalFollowing": 28,
                                "__typename": "ProfileStats"
                            },
                            "attributes": [],
                            "picture": {
                                "original": {
                                    "url": "https://statics-mumbai-lens-staging.s3.eu-west-1.amazonaws.com/profile/QmVeEwimhwaebeHFDTVY3XNjFuaNUWuhv1ksNefnzeTKXH",
                                    "__typename": "Media"
                                },
                                "__typename": "MediaSet"
                            },
                            "followModule": {
                                "__typename": "FeeFollowModuleSettings"
                            },
                            "__typename": "Profile"
                        },
                        "reaction": null,
                        "mirrors": [],
                        "hasCollectedByMe": false,
                        "onChainContentURI": "https://arweave.net/q8imNDMKotHTRsVDGP2pS6Id-dpsG_YTIbg-0x9i3Yc",
                        "canComment": {
                            "result": true,
                            "__typename": "CanCommentResponse"
                        },
                        "canMirror": {
                            "result": true,
                            "__typename": "CanMirrorResponse"
                        },
                        "canDecrypt": {
                            "result": false,
                            "reasons": [
                                "MISSING_ENCRYPTION_PARAMS"
                            ],
                            "__typename": "CanDecryptResponse"
                        },
                        "collectedBy": null,
                        "collectModule": {
                            "__typename": "RevertCollectModuleSettings"
                        },
                        "stats": {
                            "totalUpvotes": 0,
                            "totalAmountOfMirrors": 1,
                            "totalAmountOfCollects": 0,
                            "totalAmountOfComments": 5,
                            "__typename": "PublicationStats"
                        },
                        "metadata": {
                            "name": "none",
                            "description": null,
                            "content": "This one will show in all my browser tabs",
                            "image": null,
                            "attributes": [],
                            "cover": null,
                            "media": [],
                            "encryptionParams": null,
                            "__typename": "MetadataOutput"
                        },
                        "hidden": false,
                        "createdAt": "2022-12-22T19:11:59.000Z",
                        "appId": null,
                        "__typename": "Post"
                    },
                    "__typename": "Comment"
                }
            ],
            "pageInfo": {
                "totalCount": 5,
                "next": "{\"entityIdentifier\":\"0x15-0x0262\",\"timestamp\":1671944527,\"cursorDirection\":\"AFTER\"}",
                "__typename": "PaginatedResultInfo"
            },
            "__typename": "PaginatedPublicationResult"
        }
    }
}
```

## 5) Like

    (1/2 Add)

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTUxNTMsImV4cCI6MTY3MjE5Njk1M30.3pqY5eBxRleP1B8yP6hxY41jHt8SbXO_LZJjB6FsSNQ

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "operationName": "AddReaction",
    "variables": {
        "request": {
            "profileId": "0x5fc0",
            "reaction": "UPVOTE",
            "publicationId": "0x1b-0x0118"
        }
    },
    "query": "mutation AddReaction($request: ReactionRequest!) {\n  addReaction(request: $request)\n}"
}
```

---

Resp

---

```json
{
    "data": {
        "addReaction": null
    }
}
```

    (2/2 Remove)

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br
x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTUxNTMsImV4cCI6MTY3MjE5Njk1M30.3pqY5eBxRleP1B8yP6hxY41jHt8SbXO_LZJjB6FsSNQ

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "operationName": "RemoveReaction",
    "variables": {
        "request": {
            "profileId": "0x5fc0",
            "reaction": "UPVOTE",
            "publicationId": "0x1b-0x0118"
        }
    },
    "query": "mutation RemoveReaction($request: ReactionRequest!) {\n  removeReaction(request: $request)\n}"
}
```

---

Resp

---

```json
{
    "data": {
        "removeReaction": null
    }
}
```

## 6) Post

    (1/2 Upload)

BaseUrl

<https://api-testnet.lenster.xyz/metadata/upload>

---

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "version": "2.0.0",
    "metadata_id": "7a003229-7a1b-4023-8835-e3eb8478e6e1",
    "description": "Ur.....Sleepy",
    "content": "Ur.....Sleepy",
    "external_url": "https://lenster.xyz/u/davfromsecret.test",
    "image": null,
    "imageMimeType": "image/svg+xml",
    "name": "Post by @davfromsecret.test",
    "tags": [],
    "animation_url": null,
    "mainContentFocus": "TEXT_ONLY",
    "contentWarning": null,
    "attributes": [
        {
            "traitType": "type",
            "displayType": "string",
            "value": "text_only"
        }
    ],
    "media": [],
    "locale": "zh-CN",
    "appId": "Lenster"
}
```

---

Resp

---

```json
{
    "success": true,
    "id": "-Uxf5ga0cTWS29V1nZ2lLmQ0IOvKF_oI79KK-9waNu4"
}
```

    (2/2 CreatePostTypedData)

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTUxNTMsImV4cCI6MTY3MjE5Njk1M30.3pqY5eBxRleP1B8yP6hxY41jHt8SbXO_LZJjB6FsSNQ

---

Req

---

Method: `POST`

---

Body: 

```json
{
    "operationName": "CreatePostTypedData",
    "variables": {
        "options": {
            "overrideSigNonce": 2
        },
        "request": {
            "profileId": "0x5fc0",
            "contentURI": "https://arweave.net/-Uxf5ga0cTWS29V1nZ2lLmQ0IOvKF_oI79KK-9waNu4",
            "collectModule": {
                "revertCollectModule": true
            },
            "referenceModule": {
                "followerOnlyReferenceModule": false
            }
        }
    },
    "query": "mutation CreatePostTypedData($options: TypedDataOptions, $request: CreatePublicPostRequest!) {\n  createPostTypedData(options: $options, request: $request) {\n    id\n    expiresAt\n    typedData {\n      types {\n        PostWithSig {\n          name\n          type\n          __typename\n        }\n        __typename\n      }\n      domain {\n        name\n        chainId\n        version\n        verifyingContract\n        __typename\n      }\n      value {\n        nonce\n        deadline\n        profileId\n        contentURI\n        collectModule\n        collectModuleInitData\n        referenceModule\n        referenceModuleInitData\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}"
}
```

---

Resp

---

```json
{
    "data": {
        "createPostTypedData": {
            "id": "94d4e06e-52fa-4d86-82b5-3dbbb75a3bc9",
            "expiresAt": "2022-12-28T04:26:31.000Z",
            "typedData": {
                "types": {
                    "PostWithSig": [
                        {
                            "name": "profileId",
                            "type": "uint256",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "contentURI",
                            "type": "string",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "collectModule",
                            "type": "address",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "collectModuleInitData",
                            "type": "bytes",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "referenceModule",
                            "type": "address",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "referenceModuleInitData",
                            "type": "bytes",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "nonce",
                            "type": "uint256",
                            "__typename": "EIP712TypedDataField"
                        },
                        {
                            "name": "deadline",
                            "type": "uint256",
                            "__typename": "EIP712TypedDataField"
                        }
                    ],
                    "__typename": "CreatePostEIP712TypedDataTypes"
                },
                "domain": {
                    "name": "Lens Protocol Profiles",
                    "chainId": 80001,
                    "version": "1",
                    "verifyingContract": "0x60Ae865ee4C725cd04353b5AAb364553f56ceF82",
                    "__typename": "EIP712TypedDataDomain"
                },
                "value": {
                    "nonce": 2,
                    "deadline": 1672201591,
                    "profileId": "0x5fc0",
                    "contentURI": "https://arweave.net/-Uxf5ga0cTWS29V1nZ2lLmQ0IOvKF_oI79KK-9waNu4",
                    "collectModule": "0x5E70fFD2C6D04d65C3abeBa64E93082cfA348dF8",
                    "collectModuleInitData": "0x",
                    "referenceModule": "0x0000000000000000000000000000000000000000",
                    "referenceModuleInitData": "0x",
                    "__typename": "CreatePostEIP712TypedDataValue"
                },
                "__typename": "CreatePostEIP712TypedData"
            },
            "__typename": "CreatePostBroadcastItemResult"
        }
    }
}
```

## 6) Follow

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTUxNTMsImV4cCI6MTY3MjE5Njk1M30.3pqY5eBxRleP1B8yP6hxY41jHt8SbXO_LZJjB6FsSNQ

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "operationName": "ProxyAction",
    "variables": {
        "request": {
            "follow": {
                "freeFollow": {
                    "profileId": "0x01"
                }
            }
        }
    },
    "query": "mutation ProxyAction($request: ProxyActionRequest!) {\n  proxyAction(request: $request)\n}"
}
```

---

Resp

---

```json
{
    "data": {
        "proxyAction": "83e921de-76f6-480f-aa75-4a85c9265af8"
    }
}
```

## 7) Collect

Header

---

Content-Type: application/json

Accept: `*/*`

Accept-Encoding: gzip, deflate, br

x-access-token: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjB4MTlEQWVjMDA5NTVmZWNmNmE0QUM3MTU4RTM5NTM4OUNhNjY5RmI5NSIsInJvbGUiOiJub3JtYWwiLCJpYXQiOjE2NzIxOTUxNTMsImV4cCI6MTY3MjE5Njk1M30.3pqY5eBxRleP1B8yP6hxY41jHt8SbXO_LZJjB6FsSNQ

---

Req

---

Method: `POST`

Body: 

---

```json
{
    "operationName": "SuperFollow",
    "variables": {
        "request": {
            "profileId": "0x1b"
        }
    },
    "query": "query SuperFollow($request: SingleProfileQueryRequest!) {\n  profile(request: $request) {\n    id\n    followModule {\n      ... on FeeFollowModuleSettings {\n        amount {\n          asset {\n            name\n            symbol\n            decimals\n            address\n            __typename\n          }\n          value\n          __typename\n        }\n        recipient\n        __typename\n      }\n      __typename\n    }\n    __typename\n  }\n}"
}
```

---

Resp

---

```json
{
    "data": {
        "profile": {
            "id": "0x1b",
            "followModule": {
                "amount": {
                    "asset": {
                        "name": "Wrapped Matic",
                        "symbol": "WMATIC",
                        "decimals": 18,
                        "address": "0x9c3C9283D3e44854697Cd22D3Faa240Cfb032889",
                        "__typename": "Erc20"
                    },
                    "value": "1.0",
                    "__typename": "ModuleFeeAmount"
                },
                "recipient": "0x248ba21F6ff51cf0CD4765C3Bc9fAD2030a591d5",
                "__typename": "FeeFollowModuleSettings"
            },
            "__typename": "Profile"
        }
    }
}
```