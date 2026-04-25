# Azure Policy
[Azure Policy](https://learn.microsoft.com/en-us/azure/governance/policy/)

1. New policy assigned will take 5-15 minutes to take effect.
2. Policy applied restricts new resource creation and updates, but will not affect existing resource creation and updates. To apply to existing resources, you need to run a remediation task.
3. Deny Policy always takes precedence over other policies.
4. Can be assigned up-to Management group level.
5. Enforment Mode: Disabled | Enabled. Disabled doesn't mean it won't apply. It means it won't apply to new resources. To apply to existing resources, you need to run a remediation task.
6. Exemptions: You can exempt a resource from a policy assignment. When exempted, Azure Policy skips the evaluation of that resource.
7. Attestation: You can create an attestation for a policy assignment. When attested, Azure Policy will evaluate the resource against the policy assignment.
8. Managed Policies: Policy definitions created and managed by Microsoft.
9. Custom Policies: Policy definitions created by users.
10. Policy Aliases: Policy definitions created by users that are not managed by Microsoft.

## Order
[Policy Effect](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-basics)

- disabled (no enforcement, but policy definition still exists)
- append (allow the policy to update or add new values. Only applied during resource creation.)
- modify (allow the policy to update or add new values. Only applied during resource creation.)
- deny (Deny policy always takes precedence over other policies. Not allowed to create or update resources.)
- audit (Audit policy will evaluate resource, and if the policy is not met, it will audit the resource.)
- auditIfNotExists (Audit policy will evaluate resource, and if the policy is not met, it will audit the resource.)
- deployIfNotExists (Deploy policy will evaluate resource, and if the policy is not met, it will deploy the resource. This is a policy that can be used to enforce compliance with other policies.)
- manualTrigger (Manual trigger policy will trigger the remediation task manually.)

## Remediation
Remediation is a process that allows you to apply a policy assignment to existing resources. When you create a policy assignment, it will not affect existing resources. To apply the policy assignment to existing resources, you need to run a remediation task.


