---
layout: post
title: Oracle Identity Management (OIM) Certification Report Query 
---

Oracle Identity Management (OIM) helps organizations manage user access and ensure security through regular certifications. Certification queries allow you to track the progress of user access reviews. Here's a quick breakdown of a certification query in OIM and how it works.

### Sample Certification Query

```sql
SELECT DISTINCT
  cc.ID AS ID,
  cd.cert_name,
  cc.CERT_NAME AS CERTIFICATE_NAME,
  CS.PERCENT_COMPLETE AS COMPLETION_PERCENT,
  CDU.USR_LOGIN AS MANAGER,
  CDU.USR_DISPLAY_NAME AS MANAGER_USERNAME,
  CDU.USR_EMAIL AS MANAGER_EMAIL,
  COALESCE(CS.LID2_COMPL, 0) AS ACCOUNT_COMPLETED,
  COALESCE(CS.LID2_TOT, 0) AS ACCOUNT_TOTAL,
  COALESCE(CS.LID3_COMPL, 0) AS ENTITLEMENT_COMPLETED,
  COALESCE(CS.LID3_TOT, 0) AS ENTITLEMENT_TOTAL
FROM
  cert_certs CC
LEFT OUTER JOIN PRODOIM_OIM.CERTD_STATS CS ON CC.ID = CS.CERT_ID
LEFT OUTER JOIN USR CDU ON CDU.USR_KEY = CC.CERTIFIER_ID
LEFT OUTER JOIN CERT_DEFN cd ON UPPER(cc.CERT_NAME) LIKE '%' || UPPER(cd.cert_name) || '%'
WHERE
  cc.CREATEDATE > sysdate - 90
  AND LINE_ITEM_TYPE = 0
ORDER BY ID DESC;
```

### Key Points of the Query

1. **Certification Details:**
    - **ID**: Unique certification ID.
    - **Certificate Name**: Name of the certification.
    - **Completion Percentage**: How much of the certification process is done.

2. **Certifier (Manager) Information:**
    - **Manager Login/Name/Email**: Details of the manager responsible for the certification.

3. **Progress on Accounts and Entitlements:**
    - **Accounts Certified**: The number of certified user accounts.
    - **Entitlements Certified**: The number of certified permissions (entitlements) granted to users.

4. **Filtering and Sorting:**
    - The query filters certifications created in the last 90 days (`cc.CREATEDATE > sysdate - 90`).
    - Results are sorted by certification ID in descending order.

### Why This Query Matters

- **Audit & Compliance**: This query helps track the status of certifications, which is crucial for regulatory compliance (e.g., SOX, GDPR).
- **Real-time Monitoring**: Managers can easily see which certifications need attention and follow up on incomplete certifications.
- **Customizable**: The query can be adapted to focus on specific certifications, timeframes, or managers.

### Conclusion

This certification query in OIM provides a simple way to track progress on access reviews, ensuring timely completion and supporting compliance efforts. You can modify this query to suit your organization’s specific certification reporting needs.