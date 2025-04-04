Access Information:

    Keycloak: http://localhost:8080

        Admin user: admin / admin

    phpLDAPadmin: http://localhost:8081

        LDAP login: cn=admin,dc=example,dc=org / admin

    LDAP server:

        Host: openldap

        Base DN: dc=example,dc=com

        Admin DN: cn=admin,dc=example,dc=org

        Users: user01 / password1, user02 / password2

ldapsearch -x -H ldap://localhost:1389 -D "cn=admin,dc=example,dc=org" -w adminpassword -b "ou=users,dc=example,dc=org" "(objectClass=inetOrgPerson)" memberOf +


ldapadd -H ldap://localhost:1389 -D "cn=admin,dc=example,dc=org" -w "adminpassword" <<EOF
dn: cn=z-module,cn=config
objectClass: olcModuleList
cn: z-module
olcModuleLoad: dynlist.so
olcModulePath: /opt/bitnami/openldap/lib/openldap
dn: olcOverlay=dynlist,olcDatabase={N}mdb,cn=config
objectClass: olcConfig
objectClass: olcDynListConfig
objectClass: olcOverlayConfig
objectClass: top
olcOverlay: dynlist
olcDynListAttrSet: groupOfUrls memberURL member+memberOf@groupOfNames
EOF