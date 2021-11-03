- initialize vault    
`# kubectl exec vault-0 -- vault operator init -key-shares=1 -key-threshold=1 -format=json > keys.json`
- get unseal keys   
`
# VAULT_UNSEAL_KEY=$(cat keys.json | jq -r ".unseal_keys_b64[]")
# echo $VAULT_UNSEAL_KEY
`
