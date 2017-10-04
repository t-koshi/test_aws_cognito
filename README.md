```

client = Aws::CognitoIdentity::Client.new(
  region: 'ap-northeast-1',
  access_key_id: 'access_key',
  secret_access_key: 'secret_key'
)

cognitoidentityprovider = Aws::CognitoIdentityProvider::Client.new(
  region: 'ap-northeast-1',
  access_key_id: 'access_key',
  secret_access_key: 'secret_key'
)


resp = cognitoidentityprovider.sign_up({
  client_id: "xxxxxxxxxxxxxxxxxxxx", # required
  username: "UsernameType", # required
  password: "passss", # required
  user_attributes: [
    {
      name: "email",
      value: "xxx@email.com",
    },
  ],
})

resp = cognitoidentityprovider.confirm_sign_up({
  client_id: "xxxxxxx", # required
  username: "UsernameType", # required
  confirmation_code: "code", # required
  force_alias_creation: false,
})



# gem 'jwt'

require 'jwt'

client = Aws::CognitoIdentityProvider::Client.new(
  region: '',
  access_key_id: '',
  secret_access_key: ''
)

resp = client.admin_initiate_auth(
  auth_flow: 'ADMIN_NO_SRP_AUTH',
  user_pool_id: '',
  client_id: '',
  auth_parameters: {
  USERNAME: '',
  PASSWORD: ''
  }
)

respa = client.admin_respond_to_auth_challenge({
  user_pool_id: '',
  client_id: '',
  challenge_name: "",
  challenge_responses: {
    PASSWORD: '',
    USERNAME: ''
  },
  session: resp.session
})


access_token = resp.authentication_result.access_token
refresh_token = resp.authentication_result.refresh_token
id_token = resp.authentication_result.id_token

jwks = JSON.parse(open('https://cognito-idp.ap-{region}.amazonaws.com/_pool_id_/.well-known/jwks.json').read)

decode = JWT.decode id_token, nil, false

return false if decode[0]['iss'] != 'https://cognito-idp.us-east-4.amazonaws.com/{userPoolId}'

return false if decode[0]['token_use'] != 'id'

kid = decode[1]['kid']


modulus = openssl_bn(jwks['keys'][0]['n'])
exponent = openssl_bn(jwks['keys'][0]['e'])
sequence = OpenSSL::ASN1::Sequence.new(
  [OpenSSL::ASN1::Integer.new(modulus),
  OpenSSL::ASN1::Integer.new(exponent)]
)
public_key = OpenSSL::PKey::RSA.new(sequence.to_der)

```
