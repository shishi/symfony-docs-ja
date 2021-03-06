.. 2011/07/16 jptomo 1b25b0f3fee3b2ae3406c133d22037055ad3972b

.. index::
   pair: Monolog; Configuration Reference

MonologBundle 設定
=======================

.. configuration-block::

    .. code-block:: yaml

        monolog:
            handlers:

                # 設定例:
                syslog:
                    type:                stream
                    path:                /var/log/symfony.log
                    level:               ERROR
                    bubble:              false
                    formatter:           my_formatter
                main:
                    type:                fingerscrossed
                    action_level:        WARNING
                    buffer_size:         30
                    handler:             custom
                custom:
                    type:                service
                    id:                  my_handler

                # プロトタイプ
                name:
                    type:                 ~ # 必須項目
                    id:                   ~
                    priority:             0
                    level:                DEBUG
                    bubble:               true
                    path:                 %kernel.logs_dir%/%kernel.environment%.log
                    ident:                false
                    facility:             user
                    max_files:            0
                    action_level:         WARNING
                    stop_buffering:       true
                    buffer_size:          0
                    handler:              ~
                    members:              []
                    from_email:           ~
                    to_email:             ~
                    subject:              ~
                    email_prototype:
                        id:     ~ # 必須項目 (email_prototype 利用する場合)
                        method: ~
                    formatter:            ~

    .. code-block:: xml

        <container xmlns="http://symfony.com/schema/dic/services"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:monolog="http://symfony.com/schema/dic/monolog"
            xsi:schemaLocation="http://symfony.com/schema/dic/services http://symfony.com/schema/dic/services/services-1.0.xsd
                                http://symfony.com/schema/dic/monolog http://symfony.com/schema/dic/monolog/monolog-1.0.xsd">

            <monolog:config>
                <monolog:handler
                    name="syslog"
                    type="stream"
                    path="/var/log/symfony.log"
                    level="error"
                    bubble="false"
                    formatter="my_formatter"
                />
                <monolog:handler
                    name="main"
                    type="fingerscrossed"
                    action-level="warning"
                    handler="custom"
                />
                <monolog:handler
                    name="custom"
                    type="service"
                    id="my_handler"
                />
            </monolog:config>
        </container>

.. note::

    プロファイラが有効な場合、ハンドラはプロファイラで指定されたログを保存するようにします。プロファイラは "debug" を既に名前で利用しているため、この名前を設定で利用することはできません。
