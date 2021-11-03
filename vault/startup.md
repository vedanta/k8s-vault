- initialize vault    
`# kubectl exec vault-0 -- vault operator init -key-shares=1 -key-threshold=1 -format=json > keys.json`
- get unseal keys   
`# VAULT_UNSEAL_KEY=$(cat keys.json | jq -r ".unseal_keys_b64[]")`  
`# echo $VAULT_UNSEAL_KEY`  
- get root token   
`VAULT_ROOT_KEY=$(cat keys.json | jq -r ".root_token")`  
`echo $VAULT_ROOT_KEY`  
- unseal vault   
`kubectl exec vault-0 -- vault operator unseal $VAULT_UNSEAL_KEY`  
- login into vault  
`kubectl exec vault-0 -- vault login $VAULT_ROOT_KEY`  
- access from browser  
`http://<nodeport-external-ip>:32000`  
- shell into vault pod   
`kubectl exec -it vault-0 -- /bin/sh`  
