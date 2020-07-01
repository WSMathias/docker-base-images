cat samples/vulnerabilities-sample.json | jq -c '.vulnerabilities[] | select(.severity | contains("high"))'

