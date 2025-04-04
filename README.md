# Playground for experimenting with Keycloak and LDAP

## Access Information

    Keycloak: http://localhost:8080

        Admin user: admin / admin

    phpLDAPadmin: http://localhost:8081

        LDAP login: cn=admin,dc=example,dc=org / admin

    LDAP server:

        Host: openldap

        Base DN: dc=example,dc=org

        Admin DN: cn=admin,dc=example,dc=org

        Users: bob / pass, alice / pass

After starting keycloak, the LDAP password will need to be entered as this isn't included in the import

Use phpldapadmin for adding / removing users from groups.
View how that group membership is reflected (or not) in Keycloak


'''
ldapsearch -x -H ldap://localhost:1389 -D "cn=admin,dc=example,dc=org" -w admin -b "ou=users,dc=example,dc=org" "(objectClass=inetOrgPerson)" memberOf +
'''