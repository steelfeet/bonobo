# Работа с Jupyter

.. include:: _beta.rst

Существует встроенный плагин, который интегрирует (пока несколько минимально) bonobo в записные книжки jupyter, чтобы вы могли читать статус выполнения графа в красивом (хорошо, не таком уж красивом) html/javascript виджете.

## Установка

Установите `bonobo` с дополнительным пакетом **jupyter**:

```shell
pip install bonobo[jupyter]
```

Установите расширение jupyter:

```shell
jupyter nbextension enable --py --sys-prefix widgetsnbextension
jupyter nbextension enable --py --sys-prefix bonobo.contrib.jupyter
```

## Разработка

Вам следует предпочесть yarn вместо npm для установки пакетов node. Если вы предпочитаете использовать npm, адаптация кода — ваша забота.

Чтобы установить виджет для разработки, убедитесь, что вы используете редактируемую установку bonobo (см. документацию по установке):

```shell
jupyter nbextension install --py --symlink --sys-prefix bonobo.contrib.jupyter
jupyter nbextension enable --py --sys-prefix bonobo.contrib.jupyter
```

Если вы хотите изменить javascript, вы должны запустить webpack в режиме отслеживания в каком-нибудь терминале:

```shell
cd bonobo/ext/jupyter/js
yarn install
./node_modules/.bin/webpack --watch
```

Чтобы скомпилировать виджет в распространяемую версию (которая упаковывается на PyPI при выпуске), просто запустите webpack:

```shell
./node_modules/.bin/webpack
```

## Исходный код

https://github.com/python-bonobo/bonobo/tree/master/bonobo/contrib/jupyter
