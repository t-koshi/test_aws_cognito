```

client = Aws::CognitoIdentity::Client.new(
  region: 'ap-northeast-1',
  access_key_id: 'AKIAIML5WPHQYYVEKMWA',
  secret_access_key: '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'
)

cognitoidentityprovider = Aws::CognitoIdentityProvider::Client.new(
  region: 'ap-northeast-1',
  access_key_id: 'AKIAIML5WPHQYYVEKMWA',
  secret_access_key: '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'
)


resp = cognitoidentityprovider.sign_up({
  client_id: "1lnsdohbpp2u6ao6kf1se4v4fa", # required
  username: "UsernameType2", # required
  password: "Lv24aZn5!", # required
  user_attributes: [
    {
      name: "email",
      value: "koshi@guildworks.jp",
    },
  ],
})

resp = cognitoidentityprovider.confirm_sign_up({
  client_id: "1lnsdohbpp2u6ao6kf1se4v4fa", # required
  username: "UsernameType2", # required
  confirmation_code: "343580", # required
  force_alias_creation: false,
})
```
