---
title: Datadog-Chef Integration
integration_title: Chef
kind: integration
git_integration_title: chef
newhlevel: true
updated_for_agent: 5.8.5
---
# Overview

![Chef Event](/static/images/chefdashboard.png)

Connect Chef to Datadog in order to:

* Get real-time reports on Chef client runs.
* Track key Chef performance metrics across all your servers.
* Quickly identify and discuss failed Chef runs with your team

To install the Datadog Agent via Chef, please see [here][1].

[1]: http://docs.datadoghq.com/guides/chef/

# Installation

1.  If you are using Berkshelf, add the cookbook to your Berksfile:

        cookbook 'datadog'

    Otherwise, install the cookbook in to your repository using Knife:

        knife cookbook site install datadog

1.  Set the Datadog-specific attributes in either a role, environment or another recipe:

        # Make sure you replace the API and application key below
        # with the ones for your account

        node.default['datadog']['api_key'] = "9775a026f1ca7d1c6c5af9d94d9595a4"

        # Use an existing application key or create a new one for Chef
        node.default['datadog']['application_key'] ="87ce4a24b5553d2e482ea8a8500e71b8ad4554ff"

1.  Upload the updated cookbook to your Chef server

        berks upload
        # or
        knife cookbook upload datadog

        knife cookbook list | grep datadog && \
        echo -e "\033[0;32mdatadog cookbook - OK\033[0m" || \
        echo -e "\033[0;31mmissing datadog cookbook - OK\033[0m"

    The cookbook is now ready to be applied to your nodes.

1.  Once uploaded, add it to your node's run_list or role:

        "run_list": [
          "recipe[datadog::dd-handler]"
        ]

1.  Wait for the next scheduled chef-client run.

NOTE: We highly recommend that you deploy the Datadog Agent in conjunction to the Chef Handler. Further instructions on deploying the Datadog Agent via Chef can be found here.

# Metrics

<%= get_metrics_from_git() %>