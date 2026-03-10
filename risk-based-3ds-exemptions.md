---
title: Risk-based 3D Secure exemptions in payment flows
layout: doc
nav_order: 3
---

# Risk-based 3D Secure exemptions in payment flows

Risk-based 3D Secure (3DS) exemptions allow the payment system to authorize low-risk transactions without step-up authentication. The system evaluates transaction risk to determine whether to trigger 3DS or apply an exemption.

This approach maintains compliance with Strong Customer Authentication (SCA) requirements while reducing unnecessary friction.

---

## Benefits

- Reducing checkout abandonment caused by step-up authentication  
- Maintaining compliance with SCA requirements 
- Aligning authentication strength with transaction risk  
- Improving conversion rates for low-risk transactions  

---

## How it works

The payment authorization flow:

1. A customer initiates a payment transaction.
2. The payment system sends transaction details to a risk engine.
3. The risk engine evaluates signals such as:
   - Transaction amount  
   - Device characteristics  
   - Behavioral patterns  
   - Historical fraud indicators  
4. Based on risk evaluation and regulatory rules, the payment system determines whether to request a 3DS exemption.
5. The payment system submits the authorization request with an exemption indicator.
6. The issuer either approves the exemption and authorizes the transaction or requires 3DS step-up authentication.

---

## Limitations

- Issuers retain authority to require step-up authentication.  
- Exemption eligibility depends on fraud rate thresholds.  
- Regulatory requirements vary by region and change over time.  
- Inaccurate risk assessment may increase exposure to fraud. 

---

## Security and compliance considerations

To support security and compliance:

- Maintain audit logs for exemption decisions.  
- Monitor fraud rates to remain within regulatory thresholds.  
- Review exemption policies regularly.  
- Use explainable risk models during compliance reviews.  
