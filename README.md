

## About configuring **Dependabot**

You can enable **Dependabot** for any repository that uses **Dependabot alerts** and the dependency graph. For more information, see "[about dependabot security updates](/code-security/dependabot/dependabot-security-updates/about-dependabot-security-updates)."

You can enable or disable **Dependabot** for an individual repository or for all repositories owned by your personal account or organization. For more information about enabling security features in an organization, see "[securing your organization](/code-security/getting-started/securing-your-organization)."

## Supported repositories

 automatically enables **Dependabot** for newly created repositories if your personal account or organization has enabled **Automatically enable for new repositories** for **Dependabot**. For more information, see "[Managing **Dependabot** for your repositories](#managing-dependabot-security-updates-for-your-repositories)."

If you create a fork of a repository that has security updates enabled, **Github** will automatically disable **Dependabot** for the fork. You can then decide whether to enable **Dependabot** on the specific fork.

If security updates are not enabled for your repository and you don't know why, first try enabling them using the instructions given in the procedural sections below. If security updates are still not working, you can contact {% data variables.contact.contact_support %}.

## Managing **Dependabot** for your repositories

You can enable or disable **Dependabot** for all qualifying repositories owned by your personal account or organization. For more information, see "[managing personal account settings](/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-personal-account-settings/managing-security-and-analysis-settings-for-your-personal-account)" or "[managing security and analysis settings for your organizaiton](/organizations/keeping-your-organization-secure/managing-security-settings-for-your-organization/managing-security-and-analysis-settings-for-your-organization)."

You can also enable or disable **Dependabot** for an individual repository.

### Enabling or disabling **Dependabot** for an individual repository

![dependabot](https://github.com/dependabot-pypi/dependabot-pypi/assets/146808926/1066521a-62bd-41b6-8920-f4f3e6832016)

## Overriding the default behavior with a configuration file

You can override the default behavior of **Dependabot** by adding a `dependabot.yml` file to your repository. For more information, see "[configuration optoins for the dependabot](/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file)."

If you only require security updates and want to exclude version updates, you can set `open-pull-requests-limit` to `0` in order to prevent version updates for a given `package-ecosystem`. For more information, see "[dependabot version updates](/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file#open-pull-requests-limit)."

```yaml
# Example configuration file that:
#  - Has a private registry
#  - Ignores lodash dependency
#  - Disables version-updates

version: 2
registries:
  example:
    type: npm-registry
    url: https://example.com
    token: {% raw %}${{secrets.NPM_TOKEN}}{% endraw %}
updates:
  - package-ecosystem: "npm"
    directory: "/src/npm-project"
    schedule:
      interval: "daily"
    ignore:
      - dependency-name: "lodash"
        # For Lodash, ignore all updates
    # Disable version updates for npm dependencies
    open-pull-requests-limit: 0
    registries:
      - example
```

**Note:** In order for {% data variables.product.prodname_dependabot %} to use this configuration for security updates,  the `directory` must be the path to the manifest files, and you should not specify a `target-branch`.

For more information about the configuration options available for security updates, see the table in "[configuration options for dependabot](/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file#configuration-options-for-the-dependabotyml-file)."

## Further reading

- "[about dependabot alerts](/code-security/dependabot/dependabot-alerts/about-dependabot-alerts)"
- "[configuring dependabot alerts](/code-security/dependabot/dependabot-alerts/configuring-dependabot-alerts)"
- "[supply chain attacks](/code-security/supply-chain-security/understanding-your-software-supply-chain/about-the-dependency-graph#supported-package-ecosystems)"
