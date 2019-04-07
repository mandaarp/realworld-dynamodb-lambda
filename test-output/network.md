```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-imm15z@email.com",
    "username": "author-imm15z",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-imm15z@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1pbW0xNXoiLCJpYXQiOjE1NTQ2NjczOTYsImV4cCI6MTU1NDg0MDE5Nn0.n870Og7FPpGufSM5nnhHv6ZiqgFRx_nQkFIWcUes414",
    "username": "author-imm15z",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-kvfexy@email.com",
    "username": "authoress-kvfexy",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-kvfexy@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1rdmZleHkiLCJpYXQiOjE1NTQ2NjczOTYsImV4cCI6MTU1NDg0MDE5Nn0.Lp_BN0-Yj3RpYMAGlIxlWg18iwgVtHUIMqXIEkM7PQE",
    "username": "authoress-kvfexy",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author--zfvm64@email.com",
    "username": "non-author--zfvm64",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author--zfvm64@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItLXpmdm02NCIsImlhdCI6MTU1NDY2NzM5NiwiZXhwIjoxNTU0ODQwMTk2fQ.UgcZGzTfuCLdlZUJ7J0ENhUfOwXoMPEhcvbtqaf051o",
    "username": "non-author--zfvm64",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-p9zzip",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667396690,
    "updatedAt": 1554667396690,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-bv8z0e",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667396753,
    "updatedAt": 1554667396753,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-p9zzip
```
```
200 OK

{
  "article": {
    "createdAt": 1554667396690,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-p9zzip",
    "updatedAt": 1554667396690,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-bv8z0e
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1554667396753,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-bv8z0e",
    "updatedAt": 1554667396753,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/xsaod
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [xsaod]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-bv8z0e

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1554667396753,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-bv8z0e",
    "updatedAt": 1554667396753,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-bv8z0e

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1554667396753,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-bv8z0e",
    "updatedAt": 1554667396753,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-bv8z0e

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1554667396753,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-bv8z0e",
    "updatedAt": 1554667396753,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-bv8z0e

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-bv8z0e

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-bv8z0e

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-bv8z0e

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-bv8z0e]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-bv8z0e

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-imm15z]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-p9zzip/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1554667396690,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-p9zzip",
    "updatedAt": 1554667396690,
    "favoritedBy": [
      "non-author--zfvm64"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-p9zzip
```
```
200 OK

{
  "article": {
    "createdAt": 1554667396690,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-p9zzip",
    "updatedAt": 1554667396690,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-p9zzip/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-p9zzip_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-p9zzip_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-p9zzip/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1554667396690,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-p9zzip",
    "updatedAt": 1554667396690,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-p9zzip
```
```
200 OK

{}
```
```
GET /articles/title-p9zzip
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-p9zzip]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-bv8z0e
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-imm15z]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "v2wgdf",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-esjg8d",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667397903,
    "updatedAt": 1554667397903,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "v2wgdf",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dbdb3",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3vzy8a",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667397943,
    "updatedAt": 1554667397943,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dbdb3",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "mx7aq1",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wwgrb7",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667397980,
    "updatedAt": 1554667397980,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "mx7aq1",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "artw7s",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-z04x44",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398016,
    "updatedAt": 1554667398016,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "artw7s",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dnrcdk",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-eq5big",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398052,
    "updatedAt": 1554667398052,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dnrcdk",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "l7znud",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-16kj34",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398087,
    "updatedAt": 1554667398087,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "l7znud",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wm47of",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gzbt78",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398131,
    "updatedAt": 1554667398131,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wm47of",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "q0cp0o",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-er733q",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398171,
    "updatedAt": 1554667398171,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "q0cp0o",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "hytifq",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-p5yup5",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398205,
    "updatedAt": 1554667398205,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hytifq",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "xwjyvu",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gg2rkr",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398254,
    "updatedAt": 1554667398254,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "xwjyvu",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "45gw5v",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-vxje5k",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398294,
    "updatedAt": 1554667398294,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "45gw5v",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "s3bqpk",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-68zkv4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398331,
    "updatedAt": 1554667398331,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "s3bqpk",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "3urut",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title--z1yiys",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398370,
    "updatedAt": 1554667398370,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "3urut",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tvurw1",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-y9pyap",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398409,
    "updatedAt": 1554667398409,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tvurw1",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "yoxgmz",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-9xk9w8",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398454,
    "updatedAt": 1554667398454,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "yoxgmz",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7ak063",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-5nvsrn",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398476,
    "updatedAt": 1554667398476,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7ak063",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "hkra63",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2fs620",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398505,
    "updatedAt": 1554667398505,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hkra63",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tzszv8",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-5gqxab",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398544,
    "updatedAt": 1554667398544,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tzszv8",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8dadxe",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7bzebt",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398569,
    "updatedAt": 1554667398569,
    "author": {
      "username": "authoress-kvfexy",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8dadxe",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "qhkifj",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-prduk",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667398617,
    "updatedAt": 1554667398617,
    "author": {
      "username": "author-imm15z",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "qhkifj",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qhkifj",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398617,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-prduk",
      "updatedAt": 1554667398617,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8dadxe",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398569,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7bzebt",
      "updatedAt": 1554667398569,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "tzszv8"
      ],
      "createdAt": 1554667398544,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5gqxab",
      "updatedAt": 1554667398544,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hkra63",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398505,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2fs620",
      "updatedAt": 1554667398505,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7ak063",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398476,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5nvsrn",
      "updatedAt": 1554667398476,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "yoxgmz"
      ],
      "createdAt": 1554667398454,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xk9w8",
      "updatedAt": 1554667398454,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "tvurw1"
      ],
      "createdAt": 1554667398409,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y9pyap",
      "updatedAt": 1554667398409,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3urut",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398370,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--z1yiys",
      "updatedAt": 1554667398370,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s3bqpk",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398331,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-68zkv4",
      "updatedAt": 1554667398331,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "45gw5v",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398294,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vxje5k",
      "updatedAt": 1554667398294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "xwjyvu"
      ],
      "createdAt": 1554667398254,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gg2rkr",
      "updatedAt": 1554667398254,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hytifq",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398205,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p5yup5",
      "updatedAt": 1554667398205,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q0cp0o",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398171,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-er733q",
      "updatedAt": 1554667398171,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wm47of"
      ],
      "createdAt": 1554667398131,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gzbt78",
      "updatedAt": 1554667398131,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l7znud",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398087,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-16kj34",
      "updatedAt": 1554667398087,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dnrcdk",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398052,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eq5big",
      "updatedAt": 1554667398052,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "artw7s",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398016,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-z04x44",
      "updatedAt": 1554667398016,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mx7aq1",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667397980,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wwgrb7",
      "updatedAt": 1554667397980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbdb3",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667397943,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3vzy8a",
      "updatedAt": 1554667397943,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "v2wgdf"
      ],
      "createdAt": 1554667397903,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-esjg8d",
      "updatedAt": 1554667397903,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "q0cp0o",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398171,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-er733q",
      "updatedAt": 1554667398171,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "tzszv8"
      ],
      "createdAt": 1554667398544,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5gqxab",
      "updatedAt": 1554667398544,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "yoxgmz"
      ],
      "createdAt": 1554667398454,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xk9w8",
      "updatedAt": 1554667398454,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s3bqpk",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398331,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-68zkv4",
      "updatedAt": 1554667398331,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hytifq",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398205,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p5yup5",
      "updatedAt": 1554667398205,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l7znud",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398087,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-16kj34",
      "updatedAt": 1554667398087,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mx7aq1",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667397980,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wwgrb7",
      "updatedAt": 1554667397980,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-kvfexy
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8dadxe",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398569,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7bzebt",
      "updatedAt": 1554667398569,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hkra63",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398505,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2fs620",
      "updatedAt": 1554667398505,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "yoxgmz"
      ],
      "createdAt": 1554667398454,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xk9w8",
      "updatedAt": 1554667398454,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3urut",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398370,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--z1yiys",
      "updatedAt": 1554667398370,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "45gw5v",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398294,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vxje5k",
      "updatedAt": 1554667398294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hytifq",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398205,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p5yup5",
      "updatedAt": 1554667398205,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wm47of"
      ],
      "createdAt": 1554667398131,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gzbt78",
      "updatedAt": 1554667398131,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dnrcdk",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398052,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eq5big",
      "updatedAt": 1554667398052,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mx7aq1",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667397980,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wwgrb7",
      "updatedAt": 1554667397980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "v2wgdf"
      ],
      "createdAt": 1554667397903,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-esjg8d",
      "updatedAt": 1554667397903,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author--zfvm64
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-imm15z&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qhkifj",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398617,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-prduk",
      "updatedAt": 1554667398617,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "tzszv8"
      ],
      "createdAt": 1554667398544,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5gqxab",
      "updatedAt": 1554667398544,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-imm15z&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7ak063",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398476,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5nvsrn",
      "updatedAt": 1554667398476,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "tvurw1"
      ],
      "createdAt": 1554667398409,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y9pyap",
      "updatedAt": 1554667398409,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qhkifj",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398617,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-prduk",
      "updatedAt": 1554667398617,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8dadxe",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398569,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7bzebt",
      "updatedAt": 1554667398569,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "tzszv8"
      ],
      "createdAt": 1554667398544,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5gqxab",
      "updatedAt": 1554667398544,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hkra63",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398505,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2fs620",
      "updatedAt": 1554667398505,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7ak063",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398476,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5nvsrn",
      "updatedAt": 1554667398476,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "yoxgmz"
      ],
      "createdAt": 1554667398454,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xk9w8",
      "updatedAt": 1554667398454,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "tvurw1"
      ],
      "createdAt": 1554667398409,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y9pyap",
      "updatedAt": 1554667398409,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3urut",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398370,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--z1yiys",
      "updatedAt": 1554667398370,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s3bqpk",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398331,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-68zkv4",
      "updatedAt": 1554667398331,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "45gw5v",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398294,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vxje5k",
      "updatedAt": 1554667398294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "xwjyvu"
      ],
      "createdAt": 1554667398254,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gg2rkr",
      "updatedAt": 1554667398254,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hytifq",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398205,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p5yup5",
      "updatedAt": 1554667398205,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q0cp0o",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398171,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-er733q",
      "updatedAt": 1554667398171,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wm47of"
      ],
      "createdAt": 1554667398131,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gzbt78",
      "updatedAt": 1554667398131,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l7znud",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398087,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-16kj34",
      "updatedAt": 1554667398087,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dnrcdk",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398052,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eq5big",
      "updatedAt": 1554667398052,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "artw7s",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398016,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-z04x44",
      "updatedAt": 1554667398016,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mx7aq1",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667397980,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wwgrb7",
      "updatedAt": 1554667397980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbdb3",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667397943,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3vzy8a",
      "updatedAt": 1554667397943,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "v2wgdf"
      ],
      "createdAt": 1554667397903,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-esjg8d",
      "updatedAt": 1554667397903,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-kvfexy/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-kvfexy",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8dadxe",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398569,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7bzebt",
      "updatedAt": 1554667398569,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hkra63",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398505,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2fs620",
      "updatedAt": 1554667398505,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "yoxgmz"
      ],
      "createdAt": 1554667398454,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xk9w8",
      "updatedAt": 1554667398454,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3urut",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398370,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--z1yiys",
      "updatedAt": 1554667398370,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "45gw5v",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398294,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vxje5k",
      "updatedAt": 1554667398294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hytifq",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398205,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p5yup5",
      "updatedAt": 1554667398205,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wm47of"
      ],
      "createdAt": 1554667398131,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gzbt78",
      "updatedAt": 1554667398131,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dnrcdk",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398052,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eq5big",
      "updatedAt": 1554667398052,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mx7aq1",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667397980,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wwgrb7",
      "updatedAt": 1554667397980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "v2wgdf"
      ],
      "createdAt": 1554667397903,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-esjg8d",
      "updatedAt": 1554667397903,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-imm15z/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-imm15z",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qhkifj",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398617,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-prduk",
      "updatedAt": 1554667398617,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8dadxe",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398569,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7bzebt",
      "updatedAt": 1554667398569,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "tzszv8"
      ],
      "createdAt": 1554667398544,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5gqxab",
      "updatedAt": 1554667398544,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hkra63",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398505,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2fs620",
      "updatedAt": 1554667398505,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7ak063",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398476,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5nvsrn",
      "updatedAt": 1554667398476,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "yoxgmz"
      ],
      "createdAt": 1554667398454,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-9xk9w8",
      "updatedAt": 1554667398454,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "tvurw1"
      ],
      "createdAt": 1554667398409,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y9pyap",
      "updatedAt": 1554667398409,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3urut",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398370,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--z1yiys",
      "updatedAt": 1554667398370,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s3bqpk",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398331,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-68zkv4",
      "updatedAt": 1554667398331,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "45gw5v",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398294,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-vxje5k",
      "updatedAt": 1554667398294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "xwjyvu"
      ],
      "createdAt": 1554667398254,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gg2rkr",
      "updatedAt": 1554667398254,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hytifq",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398205,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p5yup5",
      "updatedAt": 1554667398205,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q0cp0o",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398171,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-er733q",
      "updatedAt": 1554667398171,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "wm47of"
      ],
      "createdAt": 1554667398131,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gzbt78",
      "updatedAt": 1554667398131,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l7znud",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667398087,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-16kj34",
      "updatedAt": 1554667398087,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dnrcdk",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667398052,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eq5big",
      "updatedAt": 1554667398052,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "artw7s",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1554667398016,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-z04x44",
      "updatedAt": 1554667398016,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "mx7aq1",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1554667397980,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wwgrb7",
      "updatedAt": 1554667397980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbdb3",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1554667397943,
      "author": {
        "username": "author-imm15z",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3vzy8a",
      "updatedAt": 1554667397943,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "v2wgdf"
      ],
      "createdAt": 1554667397903,
      "author": {
        "username": "authoress-kvfexy",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-esjg8d",
      "updatedAt": 1554667397903,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "dbdb3",
    "tag_1",
    "tag_mod_2_1",
    "tag_mod_3_1",
    "tag_a",
    "tag_b",
    "dnrcdk",
    "tag_4",
    "tag_mod_2_0",
    "8dadxe",
    "tag_18",
    "tag_mod_3_0",
    "7ak063",
    "tag_15",
    "tag_13",
    "tvurw1",
    "hytifq",
    "tag_8",
    "tag_mod_3_2",
    "3urut",
    "tag_12",
    "45gw5v",
    "tag_10",
    "tag_17",
    "tzszv8",
    "tag_9",
    "xwjyvu",
    "hkra63",
    "tag_16",
    "q0cp0o",
    "tag_7",
    "qhkifj",
    "tag_19",
    "tag_6",
    "wm47of",
    "mx7aq1",
    "tag_2",
    "tag_14",
    "yoxgmz",
    "tag_0",
    "v2wgdf",
    "l7znud",
    "tag_5",
    "artw7s",
    "tag_3",
    "s3bqpk",
    "tag_11"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-autcbq@email.com",
    "username": "author-autcbq",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-autcbq@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1hdXRjYnEiLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.gAhUX-nQw8NmeKbFmI0TV8SFS-41cV3l_ckZUPMosLU",
    "username": "author-autcbq",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-lczt9g@email.com",
    "username": "commenter-lczt9g",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-lczt9g@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1sY3p0OWciLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.EPIlGGT-im5yMbUybnZdFgB1RkwjuiwfVMvqSAj_yI8",
    "username": "commenter-lczt9g",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-qqy3jt",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1554667400154,
    "updatedAt": 1554667400154,
    "author": {
      "username": "author-autcbq",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment yt8ptc"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "60309f99-65d8-499f-a824-cb3b9cd4f993",
    "slug": "title-qqy3jt",
    "body": "test comment yt8ptc",
    "createdAt": 1554667400186,
    "updatedAt": 1554667400186,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment mcmqwj"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "62f2468e-c94a-42c1-9c0d-2e1b243cd793",
    "slug": "title-qqy3jt",
    "body": "test comment mcmqwj",
    "createdAt": 1554667400231,
    "updatedAt": 1554667400231,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment waz6ba"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "c2d356e1-68b8-4d22-abd5-b847e0734560",
    "slug": "title-qqy3jt",
    "body": "test comment waz6ba",
    "createdAt": 1554667400262,
    "updatedAt": 1554667400262,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment bqyq1r"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "bb8f6a02-aaea-47da-ace5-0a38efc2e741",
    "slug": "title-qqy3jt",
    "body": "test comment bqyq1r",
    "createdAt": 1554667400294,
    "updatedAt": 1554667400294,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment ewhozn"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "c6812e70-7763-45b0-aafc-0f79ff05aaab",
    "slug": "title-qqy3jt",
    "body": "test comment ewhozn",
    "createdAt": 1554667400327,
    "updatedAt": 1554667400327,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment o54uj5"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e0911d89-298a-44cd-83ca-961671cbf4a3",
    "slug": "title-qqy3jt",
    "body": "test comment o54uj5",
    "createdAt": 1554667400357,
    "updatedAt": 1554667400357,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment fmsaup"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ab8a4801-1b48-4d2e-9013-3d089d090416",
    "slug": "title-qqy3jt",
    "body": "test comment fmsaup",
    "createdAt": 1554667400400,
    "updatedAt": 1554667400400,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment kwibix"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "75d41a6e-8826-45b0-b36b-7c30bf634e17",
    "slug": "title-qqy3jt",
    "body": "test comment kwibix",
    "createdAt": 1554667400439,
    "updatedAt": 1554667400439,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment 9e0sow"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "90511a51-b334-42c6-a4ba-0b1de21b422f",
    "slug": "title-qqy3jt",
    "body": "test comment 9e0sow",
    "createdAt": 1554667400472,
    "updatedAt": 1554667400472,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-qqy3jt/comments

{
  "comment": {
    "body": "test comment fzlj40"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "d49c45b2-7d3b-4640-a4e1-6e7441a7f5a5",
    "slug": "title-qqy3jt",
    "body": "test comment fzlj40",
    "createdAt": 1554667400505,
    "updatedAt": 1554667400505,
    "author": {
      "username": "commenter-lczt9g",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-qqy3jt/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-qqy3jt/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment vbxqa0"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-qqy3jt/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1554667400231,
      "id": "62f2468e-c94a-42c1-9c0d-2e1b243cd793",
      "body": "test comment mcmqwj",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400231
    },
    {
      "createdAt": 1554667400262,
      "id": "c2d356e1-68b8-4d22-abd5-b847e0734560",
      "body": "test comment waz6ba",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400262
    },
    {
      "createdAt": 1554667400357,
      "id": "e0911d89-298a-44cd-83ca-961671cbf4a3",
      "body": "test comment o54uj5",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400357
    },
    {
      "createdAt": 1554667400400,
      "id": "ab8a4801-1b48-4d2e-9013-3d089d090416",
      "body": "test comment fmsaup",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400400
    },
    {
      "createdAt": 1554667400439,
      "id": "75d41a6e-8826-45b0-b36b-7c30bf634e17",
      "body": "test comment kwibix",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400439
    },
    {
      "createdAt": 1554667400186,
      "id": "60309f99-65d8-499f-a824-cb3b9cd4f993",
      "body": "test comment yt8ptc",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400186
    },
    {
      "createdAt": 1554667400294,
      "id": "bb8f6a02-aaea-47da-ace5-0a38efc2e741",
      "body": "test comment bqyq1r",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400294
    },
    {
      "createdAt": 1554667400505,
      "id": "d49c45b2-7d3b-4640-a4e1-6e7441a7f5a5",
      "body": "test comment fzlj40",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400505
    },
    {
      "createdAt": 1554667400472,
      "id": "90511a51-b334-42c6-a4ba-0b1de21b422f",
      "body": "test comment 9e0sow",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400472
    },
    {
      "createdAt": 1554667400327,
      "id": "c6812e70-7763-45b0-aafc-0f79ff05aaab",
      "body": "test comment ewhozn",
      "slug": "title-qqy3jt",
      "author": {
        "username": "commenter-lczt9g",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1554667400327
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-qqy3jt/comments/60309f99-65d8-499f-a824-cb3b9cd4f993
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-qqy3jt/comments/62f2468e-c94a-42c1-9c0d-2e1b243cd793
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-lczt9g]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-qqy3jt/comments/62f2468e-c94a-42c1-9c0d-2e1b243cd793
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-qqy3jt/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.7oseu4pv64j@email.com",
    "username": "user1-0.7oseu4pv64j",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.7oseu4pv64j@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN29zZXU0cHY2NGoiLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.qd3ShEI_DjGBHoq7lwWzicLux0Oo9oXAXfR2C7OW468",
    "username": "user1-0.7oseu4pv64j",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.7oseu4pv64j@email.com",
    "username": "user1-0.7oseu4pv64j",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.7oseu4pv64j]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.7oseu4pv64j@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.7oseu4pv64j@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.7oseu4pv64j@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.7oseu4pv64j@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN29zZXU0cHY2NGoiLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.qd3ShEI_DjGBHoq7lwWzicLux0Oo9oXAXfR2C7OW468",
    "username": "user1-0.7oseu4pv64j",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.g19stgzep6h",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.g19stgzep6h]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.7oseu4pv64j@email.com",
    "password": "0.m7vh0d5yc79"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.7oseu4pv64j@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN29zZXU0cHY2NGoiLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.qd3ShEI_DjGBHoq7lwWzicLux0Oo9oXAXfR2C7OW468",
    "username": "user1-0.7oseu4pv64j",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.7oseu4pv64j
```
```
200 OK

{
  "profile": {
    "username": "user1-0.7oseu4pv64j",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.bbsjp7wknnp
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.bbsjp7wknnp]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1NTQ2Njc0MDEsImV4cCI6MTU1NDg0MDIwMX0.GvkdK3lU0Uhetko6qvvedrdvFhbdxhzgzO3SaIgg10M",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.h7wsjn7db7m",
    "email": "user2-0.h7wsjn7db7m@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.h7wsjn7db7m@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuaDd3c2puN2RiN20iLCJpYXQiOjE1NTQ2Njc0MDEsImV4cCI6MTU1NDg0MDIwMX0.l3lqCkUiWluhT-IAiAk8Peu1aQ_h1ZOf3O2BNyx_XGU",
    "username": "user2-0.h7wsjn7db7m",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.7oseu4pv64j@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.7oseu4pv64j",
    "email": "updated-user1-0.7oseu4pv64j@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN29zZXU0cHY2NGoiLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.qd3ShEI_DjGBHoq7lwWzicLux0Oo9oXAXfR2C7OW468"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.7oseu4pv64j",
    "email": "updated-user1-0.7oseu4pv64j@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN29zZXU0cHY2NGoiLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.qd3ShEI_DjGBHoq7lwWzicLux0Oo9oXAXfR2C7OW468"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.7oseu4pv64j",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN29zZXU0cHY2NGoiLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.qd3ShEI_DjGBHoq7lwWzicLux0Oo9oXAXfR2C7OW468"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.7oseu4pv64j",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN29zZXU0cHY2NGoiLCJpYXQiOjE1NTQ2Njc0MDAsImV4cCI6MTU1NDg0MDIwMH0.qd3ShEI_DjGBHoq7lwWzicLux0Oo9oXAXfR2C7OW468"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.ivhx5zcfze@email.com",
    "username": "user2-0.ivhx5zcfze",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.ivhx5zcfze@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuaXZoeDV6Y2Z6ZSIsImlhdCI6MTU1NDY2NzQwMSwiZXhwIjoxNTU0ODQwMjAxfQ.PQRVcK3BycBlMDoMwc9bzIgAzKh99qubRPxgDmz0PDM",
    "username": "user2-0.ivhx5zcfze",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.ivhx5zcfze@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.ivhx5zcfze@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2019-04-07T20:03:21.573Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
