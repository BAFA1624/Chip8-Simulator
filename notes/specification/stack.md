# The Stack

[[toc]]

The stack is only used to store return addresses when subroutines are called. The original RCA 1802 version allocated 48 bytes for up to 12 levels of nesting; modern implementations usually have more.

## Design

### Requirements
- [ ] At least 12 levels of nesting.
- [ ] push\_front
- [ ] push\_back
- [ ] pop\_front
- [ ] pop\_back
