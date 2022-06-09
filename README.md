# Ckan SSO 教學 with Keycloak and ckanext-saml2auth
## Ckan 安裝
請參照[CKAN官方教學](http://docs.ckan.org/en/2.9/maintaining/installing/index.html)，這邊建議使用Installing CKAN from source的方式安裝，在未來設定Ckan、安裝插件會較好操作。
## Keycloak 安裝
請參照[Keycloak官方教學](https://www.keycloak.org/guides#getting-started)，我們這邊使用docker架設。
## Ckan 插件 saml2auth 安裝
請參照[saml2auth](https://github.com/keitaroinc/ckanext-saml2auth)中的教學安裝，這邊需要上述Installing CKAN from source的方式安裝CKAN會較方便操作，並將Config settings 中 Required 的設定複製到 Ckan 設定檔中，例 /etc/ckan/default/ckan.ini
## Keycloak 設定
- 首先，新增一個 Realm，若已有使用中的 Realm 則看自己的需求
![Add Realm][1]
- 接著創建一個 Client，Protocol 選擇 saml
![Create Client 1][2]
![Create Client 2][3]
- 再來需要進入剛才創建的 Client 設定 Mapper，讓 Ckan 能夠取到相對應的資料，並更改或記下 SAML Attribute Name 以便待會 Ckan 設定使用
![Config Client's Mapper][4]
![Config Client's Mapper][5]
![Config Client's Mapper][6]
![Config Client's Mapper][7]
![Config Client's Mapper][8]
- 接著在 Realm Settings 點進 SAML 2.0 Identity Provider Metadata 連結，並將進去後的網頁另存新檔成 xml 檔，以便後續 Ckan 設定使用
![Metadata][9]
## Ckan 設定
- 在 Ckan 設定檔中，更改 ckanext-saml2auth 的設定。
```ini
#將此設定改成local
ckanext.saml2auth.idp_metadata.location = local
#獎此設定改成上面儲存的xml
ckanext.saml2auth.idp_metadata.local_path = /opt/metadata/idp.xml

#並將以下設定改成上面 Mapper 設定的 SAML Attribute Name

ckanext.saml2auth.user_firstname = firstname

ckanext.saml2auth.user_lastname = lastname

ckanext.saml2auth.user_email = email

#並將以下設定為上面創建 Client 的 Client ID 
ckanext.saml2auth.entity_id = tutorial
```

[1]: https://i.imgur.com/EpRfK5W.jpg
[2]: https://i.imgur.com/BpgPR5m.jpg
[3]: https://i.imgur.com/PJoovW6.jpg
[4]: https://i.imgur.com/tcTiQPm.jpg
[5]: https://i.imgur.com/74BnklR.jpg
[6]: https://i.imgur.com/F526Sul.jpg
[7]: https://i.imgur.com/0R5w1Tg.jpg
[8]: https://i.imgur.com/iyRuD74.jpg
[9]: https://i.imgur.com/DAw0zs2.jpg
