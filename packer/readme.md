`Форк https://github.com/timurb/otus-packer`

**Описания**
Домашка от отус, во время которой был создан образ в Google Compute и Yandex Cloud.

**Инструкция**
1. Установите Yandex.CLI: https://cloud.yandex.ru/docs/cli/operations/install-cli
2. Установите Packer: https://www.packer.io/
3. Подключитесь при помощи Yandex.CLI к облаку и просмотрите конфигурацию: yc init yc config list
4. Создайте сервисную учетную запись для packer: `yc iam service-account create --name packer --folder-id XXXXXXXXXXXXX` `yc iam service-account get` `yc resource-manager folder add-access-binding --id XXXXXXXXXXXXX --role editor --service-account-id XXXXXXXXXXXXXXX` `yc iam key create --service-account-id XXXXXXXXXXXXXXX --output key.json`
5. Вставьте путь к вашему ключу в template.json в "service_account_key_file" в блок builders и создайте из этого шаблона образ (вероятно понадобится удалить из шаблона параметр token)
6. Из файла variables.auto.json.example создайте и заполните файл variables.auto.json
7. Создайте у себя в облаке образ: `packer build json/template.json`