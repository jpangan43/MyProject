# Microsoft Teams Configuration

This guide documents key Microsoft Teams and Microsoft 365 Groups governance settings illustrated by the provided screenshots.

## Overview

Proper Teams governance helps keep the environment clean, secure, and easy to manage by controlling:

- Team and group naming
- Group / Team expiration and lifecycle
- Channel structure examples

## 1. Example Team with Channels

A well-structured Team typically contains:

- A **General** channel (created by default)
- Additional standard or private channels for projects, departments, or topics
- Clear naming conventions so users can quickly find the right place to collaborate

![Example Team with Channels](../extracted/Teams/1-Example-Team-with-Channels.png)

---

## 2. Group Expiration Policy

Microsoft 365 Groups (and the Teams that are backed by them) can be configured with an expiration policy. This automatically deletes or notifies owners of inactive groups after a defined period, reducing clutter.

Typical configuration points:

- Enable group expiration
- Set the lifetime (e.g., 180 or 365 days)
- Define the notification / renewal behavior
- Choose which groups the policy applies to (all groups or specific groups)

![Group Expiration Policy](../extracted/Teams/2-Group-Expiration-Policy.png)

---

## 3. Naming Policy Configuration

A group naming policy enforces consistent naming for Microsoft 365 Groups and Teams. It can:

- Add a prefix and/or suffix (static text or attributes such as department, country, etc.)
- Block specific words (profanity, reserved terms, etc.)

This improves searchability and prevents confusing or non-compliant names.

![Naming Policy Configuration](../extracted/Teams/3-Naming-Policy-Configuration.png)

> Tip: The blocked words list can be maintained via a CSV (see the companion Intune / M365 configuration package for an example `BlockedWords.csv`).

---

## 4. Teams List Overview

After policies are applied you can review the list of Teams in the Teams admin center or Microsoft 365 admin center. The list shows:

- Team name
- Visibility (Public / Private)
- Owner(s)
- Member count
- Status / activity indicators

![Teams List](../extracted/Teams/4-Teams-List.png)

---

## Recommended Governance Checklist

| Setting                    | Recommendation                                      |
|---------------------------|-----------------------------------------------------|
| Group expiration          | Enable (e.g., 365 days) with owner notifications    |
| Naming policy             | Prefix + blocked words list                         |
| Creation permissions      | Limit who can create Teams / Groups if needed       |
| Guest access              | Review and restrict according to security policy    |
| Sensitivity labels        | Apply labels that control external sharing          |
| Retention policies        | Align with organizational data-retention requirements |

## Related Guides

- [Configure Custom Domain](Configure-Custom-Domain.md)
- [Configure DNS](Configure-DNS.md)
- [Configure Microsoft Intune](Configure-Microsoft-Intune.md)
