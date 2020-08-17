# notify_peers

notify_peers is a BGP peering maintenance Ansible module. It sends out notification emails to peers NOCs when BGP sessions towards them are down and a summary of it all to your NOC email.

## How does it work?

Very simply, it works like this:

- ansible_notify_peers_playbook.yml:
  - calls subplaybook based on router OS (extreme SLXOS support for now only i.e. ansible_notify_peers_extreme.yml)
  - connects to the router with ansible to get the CLI output equivalent of "show ip bgp summary"
  - passes the output to the homemade Ansible module in library/slx_command
    - parses the output to get a list of peers that are down
    - goes through the list and makes a list of peer objects
    - goes through the list of peers to fill NOC email and company name fields through peeringdb.com API calls based on ASN
      [optional]
    - goes through the list of peers to send a personalized E-mail to the remote ASN asking for checking the peering session
    - sends a report to your own NOC
      [/optional

## Support

For now the script supports following router CLI type:
- SLXOS

## Todo
- add BGP session down duration min threshold to avoid alerting flapping ASs
- add brocade support
- add huawei support

