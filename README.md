# get-open-pull-requests

**Abandoned** Use Octokit.

Module to get open PRs from GitHub API.
Useful for things like a recurring Slack notification.

--------

## Installation

`npm i get-open-pull-requests`

## Usage

#### Get a Token

Go to <https://github.com/settings/tokens> and get a token that allows user read
access. If you're setting this up for an org, allow org read access.

#### Use It

```javascript
const prs = require('get-open-pull-requests')
const config = {
  api: '', // github enterprise url, or defaults to api.github.com
  user: '', // user or org slug. example: zautumnz
  token: '', // github access token, see below
}

prs(config).then((a) => JSON.stringify(a, null, 2)).then(console.log)

// returns { url, labels, user, title }
// example:
// {
//   url: 'https://github.com/zautumnz/styled-reset/pull/9999',
//   title: 'Does a thing',
//   user: 'zautumnz',
//   labels: [ 'totally-real-pr', 'discussion' ]
// }

// slack formatting example:

const format = (p) =>
  `*${p.title}* - _${p.user}_ - (<${p.url}>)
  ${p.labels.join(', ')}
  `.trim()

prs(config)
  .then((res) => res.map(format).join('\n\n'))
  .then(sendToSlackOrSomething)
```

[LICENSE](./LICENSE.md)
