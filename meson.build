project('discord-rpc', ['cpp'],
    default_options : [
        'cpp_std=c++14',
        'cpp_eh=none'
    ]
    version : '3.5',
    license : 'Discord Inc'
)

sources = [
    'src/discord_rpc.cpp',
    'src/rpc_connection.cpp',
    'src/serialization.cpp'
]

headers = [
    'include/discord_rpc.h',
    'include/discord_register.h'
]

args = []
links = []
deps = []

incs = [
    include_directories('')
]

if host_machine.system() == 'windows'
    args += [
        '/DDISCORD_WINDOWS',
        '/Wall',
        '/wd4100',
        '/wd4514',
        '/wd4625',
        '/wd5026',
        '/wd4626',
        '/wd4668',
        '/wd4710',
        '/wd4710',
        '/wd4711',
        '/wd4820',
        '/wd4946',
        '/wd5027'
    ]
    sources += [
        'src/connection_win.cpp',
        'src/discord_register_win.cpp'
    ]
    links += [
        'psapi.lib',
        'advapi.lib'
    ]
elif host_machine.system() == 'darwin'
    args += '-DDISCORD_OSX'
    sources += 'src/discord_register_osx.m'
    deps += dependency('appleframework', modules : 'AppKit')
else
    args += '-DDISCORD_LINUX'
endif