# Playground for experimenting with Keycloak and LDAP

## Access Information

### Keycloak
http://localhost:8080
Admin user: admin / admin

### phpLDAPadmin
http://localhost:8081
LDAP login: cn=admin,dc=example,dc=org / admin


Users: bob / pass, alice / pass, carol / pass

Use phpldapadmin for adding / removing users from groups.
View how that group membership is reflected (or not) in Keycloak

Logging in with the users can be done at http://localhost:8080/realms/test/account

When exporting the realm JSON, remember to tick include clients otherwise the above account app will break.
Also set "bindCredential" in the exported JSON as this is set to a dummy value.

'''
ldapsearch -x -H ldap://localhost:1389 -D "cn=admin,dc=example,dc=org" -w admin -b "ou=users,dc=example,dc=org" "(objectClass=inetOrgPerson)" memberOf +
'''

### User Federation LDAP settings
connection URL
ldap://openldap:1389

Bind DN cn=admin,dc=example,dc=org

Edit mode READ_ONLY

Users DN ou=users,dc=example,dc=org

User object classes inetOrgPerson

UUID LDAP attribute
entryUUID

### ldap group mapper Settings

LDAP Groups DN
ou=groups,dc=example,dc=org

Group Object Classes
groupOfUniqueNames

Membership LDAP Attribute
uniqueMember

Mode READ_ONLY

User Groups Retrieve Strategy
GET_GROUPS_FROM_MEMBEROF_ATTRIBUTE

Drop non-existing groups during sync
ON