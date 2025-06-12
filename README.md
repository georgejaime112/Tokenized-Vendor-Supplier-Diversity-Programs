# Tokenized Vendor Supplier Diversity Programs

A comprehensive blockchain-based system for managing supplier diversity programs using Clarity smart contracts on the Stacks blockchain.

## Overview

This system provides a complete solution for organizations to manage their supplier diversity initiatives through transparent, automated, and verifiable smart contracts. The platform enables diversity officer verification, supplier certification, opportunity matching, performance tracking, and automated reporting.

## Features

### 🏛️ Diversity Officer Verification
- Secure verification process for diversity officers
- Credential validation and expiration management
- Role-based access control for certification activities

### 🏢 Supplier Certification
- Multi-category diversity certification (Minority, Women, Veteran, Disability, LGBTQ+ owned)
- Document verification and compliance tracking
- Revenue tier classification for targeted opportunities

### 🤝 Opportunity Matching
- Automated matching of certified suppliers with opportunities
- Bid management and proposal tracking
- Transparent award process with audit trails

### 📊 Performance Tracking
- Comprehensive supplier performance metrics
- Contract completion rates and quality ratings
- Performance scoring algorithm for supplier ranking

### 📈 Reporting Automation
- Automated diversity spend reporting
- Compliance report generation
- Period-based metrics and analytics

## Smart Contracts

### 1. Diversity Officer Verification (`diversity-officer-verification.clar`)
Manages the verification and lifecycle of diversity officers who can certify suppliers.

**Key Functions:**
- `submit-verification`: Submit credentials for officer verification
- `verify-officer`: Verify an officer (owner only)
- `is-verified-officer`: Check if an officer is currently verified
- `revoke-verification`: Revoke officer verification

### 2. Supplier Certification (`supplier-certification.clar`)
Handles the certification process for diverse suppliers across multiple categories.

**Key Functions:**
- `apply-for-certification`: Submit application for diversity certification
- `certify-supplier`: Certify a supplier (verified officers only)
- `is-certified-supplier`: Check if supplier is currently certified
- `revoke-certification`: Revoke supplier certification

**Diversity Categories:**
- `1`: Minority Owned Business Enterprise (MBE)
- `2`: Women Owned Business Enterprise (WBE)
- `3`: Veteran Owned Small Business (VOSB)
- `4`: Disability Owned Business Enterprise (DOBE)
- `5`: LGBTQ+ Owned Business Enterprise

### 3. Opportunity Matching (`opportunity-matching.clar`)
Facilitates the creation and management of procurement opportunities for diverse suppliers.

**Key Functions:**
- `create-opportunity`: Create new procurement opportunity
- `apply-for-opportunity`: Submit application for opportunity
- `award-opportunity`: Award opportunity to winning supplier
- `get-opportunity`: Retrieve opportunity details

### 4. Performance Tracking (`performance-tracking.clar`)
Tracks and manages supplier performance metrics and contract outcomes.

**Key Functions:**
- `record-contract`: Record new contract for supplier
- `complete-contract`: Mark contract as completed with rating
- `get-supplier-performance`: Retrieve supplier performance metrics
- `get-contract-record`: Get specific contract details

### 5. Reporting Automation (`reporting-automation.clar`)
Automates the generation of diversity reports and compliance documentation.

**Key Functions:**
- `generate-report`: Generate diversity report for a period
- `submit-compliance-report`: Submit compliance documentation
- `get-diversity-report`: Retrieve diversity report
- `calculate-diversity-score`: Calculate diversity percentage

## Installation

### Prerequisites
- [Clarinet](https://github.com/hirosystems/clarinet) for local development
- [Node.js](https://nodejs.org/) for running tests
- [Stacks CLI](https://docs.stacks.co/docs/cli) for deployment

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd supplier-diversity-program
```

2. Install dependencies:
```bash
npm install
```

3. Initialize Clarinet project:
```bash
clarinet new supplier-diversity
cd supplier-diversity
```

4. Copy contract files to the contracts directory
5. Copy test files to the tests directory

## Testing

Run the test suite using Vitest:

```bash
npm test
```

Run specific test files:
```bash
npm test diversity-officer-verification.test.js
npm test supplier-certification.test.js
npm test opportunity-matching.test.js
npm test performance-tracking.test.js
npm test reporting-automation.test.js
```

## Usage

### 1. Officer Verification Process

1. **Submit Verification**: Diversity officers submit their credentials
```clarity
(contract-call? .diversity-officer-verification submit-verification "Organization Name" 0x...)
```

2. **Verify Officer**: Contract owner verifies the officer
```clarity
(contract-call? .diversity-officer-verification verify-officer 'SP... "Organization Name")
```

### 2. Supplier Certification Process

1. **Apply for Certification**: Suppliers submit certification applications
```clarity
(contract-call? .supplier-certification apply-for-certification "Business Name" u1 0x... u2)
```

2. **Certify Supplier**: Verified officers certify suppliers
```clarity
(contract-call? .supplier-certification certify-supplier 'SP...)
```

### 3. Opportunity Management

1. **Create Opportunity**: Organizations create procurement opportunities
```clarity
(contract-call? .opportunity-matching create-opportunity "Title" "Description" u50000 u1 u2000)
```

2. **Apply for Opportunity**: Certified suppliers submit applications
```clarity
(contract-call? .opportunity-matching apply-for-opportunity u1 0x... u45000)
```

### 4. Performance Tracking

1. **Record Contract**: Track new contracts
```clarity
(contract-call? .performance-tracking record-contract 'SP... u25000)
```

2. **Complete Contract**: Mark contracts as completed with ratings
```clarity
(contract-call? .performance-tracking complete-contract 'SP... u1 u4)
```

### 5. Generate Reports

1. **Generate Diversity Report**: Create automated diversity reports
```clarity
(contract-call? .reporting-automation generate-report u1 u1000000 u250000 u50 u15 (list u5 u3 u4 u2 u1))
```

## Error Codes

### Diversity Officer Verification
- `100`: Unauthorized access
- `101`: Officer already verified
- `102`: Officer not found
- `103`: Invalid credentials

### Supplier Certification
- `200`: Unauthorized access
- `201`: Supplier already certified
- `202`: Application not found
- `203`: Invalid diversity category
- `204`: Officer not verified

### Opportunity Matching
- `300`: Unauthorized access
- `301`: Opportunity not found
- `302`: Already applied
- `303`: Opportunity closed
- `304`: Supplier not certified

### Performance Tracking
- `400`: Unauthorized access
- `401`: Record not found
- `402`: Invalid score/rating

### Reporting Automation
- `500`: Unauthorized access
- `501`: Report already exists
- `502`: Report not found

## Security Considerations

1. **Access Control**: Only verified diversity officers can certify suppliers
2. **Data Integrity**: All critical data is stored on-chain with hash verification
3. **Expiration Management**: Certifications and verifications have expiration dates
4. **Audit Trail**: All actions are recorded with timestamps and actor information

## Contributing

1. Fork the repository
2. Create a feature branch
3. Write tests for new functionality
4. Ensure all tests pass
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For questions or support, please open an issue in the repository or contact the development team.

## Roadmap

- [ ] Integration with external identity verification services
- [ ] Mobile application for supplier management
- [ ] Advanced analytics dashboard
- [ ] Multi-chain deployment support
- [ ] API gateway for third-party integrations
```
