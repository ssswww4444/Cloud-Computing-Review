# Lecture 12.1 Security and Clouds

#### Why is security so important？
* If system (Grids/Clouds/outsourced infrastructure) not secure
    * 如果有安全问题，大团体就不会使用，要重复实验很expensive，有法律道德问题，丢失信任
    1. Large communities will not engage
        * or rather they will only use their own internal resources
    2. Expensive (impossible?) to repeat some experiments
        * Huge machines running large simulations for several years
    3. Legal and ethical issues possible to be violated with all sort of consequences
    4. Trust is easily lost and hard to re-establish
* Note: security technology ≠ secure system
    * 无法保证secure system

#### Technical Challenges of Security (7)
* Generally speaking
    1. Authentication 身份验证
    2. Authorisation
    3. Audit/accounting
* Domain specific
    1. Confidentiality
    2. Privacy
* Inter-organisational and Technological challenge
    1. Fabric management
    2. Trust

#### Authentication
* **Establishment and propagation** of a user's identity in the system
    * Centralised v.s. Decentralised systems
    * Public Key Infrastructure (PKI) (用public key的整套系统)
        * underpins MANY systems
        * based on public key cryptography
* Public Key Cryptography 
    * aka. Asymmetric Cryptography (Public & Private keys)
    * Two distinct keys
        1. Private Key
        2. Public Key
    * Two keys complementary
        * cannot find out value of a private key from public key
        * with private key, can digitally sign messages, documents, ..., and validate them with associated public keys
    * Simplifies key management
        * don't need to have many keys for long time
* Public key Certificate
    * 看这个public key属于谁的，由认证机构发放
    * Mechanism connecting public key to user with corresponding private key
    * Issued by **trusted "Certification Authority"**

#### Certification Authority (CA)
* **Central component** of Public Key Infrastructure (PKI)
* CA has numerous responsibilities:
    1. Policy and procedure
        * processes that should be followed by users, organisation, 
    2. Issuing certificates
    3. Revoking certificates
    4. Storing, archiving