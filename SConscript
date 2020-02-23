Import('RTT_ROOT')
from building import *

# get current directory
cwd = GetCurrentDir()

# The set of source files associated with this SConscript file.
src = Glob('common/*.c')
src += Glob('mqtt/*.c')
src += Glob('mqttclient/*.c')
src += Glob('network/*.c')
src += Glob('platform/RT-Thread/*.c')

if GetDepend(['PKG_USING_MQTTCLIENT_TEST']):
    src += Glob('tests/*.c')

path = [cwd + '/common']
path += [cwd + '/mqtt']
path += [cwd + '/mqttclient']
path += [cwd + '/network']
path += [cwd + '/platform/RT-Thread']

if GetDepend(['LOG_IS_SALOF']):
    src += Glob('common/log/*.c')
    src += Glob('common/log/arch/rt-thread/*.c')
    path += [cwd + '/common/log']
    group = DefineGroup('mqttclient/log', Glob('common/log/*.c'), depend = ['PKG_USING_MQTTCLIENT'])
    group = DefineGroup('mqttclient/log', Glob('common/log/arch/rt-thread/*.c'), depend = ['PKG_USING_MQTTCLIENT'])

if GetDepend(['MQTT_NETWORK_TYPE_TLS']):
    src += Glob('common/mbedtls/library/*.c')
    src += Glob('common/mbedtls/wrapper/*.c')
    path += [cwd + '/common/mbedtls/wrapper']
    path += [cwd + '/common/mbedtls/include']
    path += [cwd + '/common/mbedtls/include/mbedtls']
    group = DefineGroup('mbedtls/library', Glob('common/mbedtls/library/*.c'), depend = ['PKG_USING_MQTTCLIENT'])
    group = DefineGroup('mbedtls/wrapper', Glob('common/mbedtls/wrapper/*.c'), depend = ['PKG_USING_MQTTCLIENT'])

group = DefineGroup('mqttclient', Glob('mqttclient/*.c'), depend = ['PKG_USING_MQTTCLIENT'])
group = DefineGroup('mqttclient/common', Glob('common/*.c'), depend = ['PKG_USING_MQTTCLIENT'])
group = DefineGroup('mqttclient/mqtt', Glob('mqtt/*.c'), depend = ['PKG_USING_MQTTCLIENT'])
group = DefineGroup('mqttclient/network', Glob('network/*.c'), depend = ['PKG_USING_MQTTCLIENT'])
group = DefineGroup('mqttclient/platform', Glob('platform/RT-Thread/*.c'), depend = ['PKG_USING_MQTTCLIENT'], CPPPATH = path)

Return('group')
