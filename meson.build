project('discord-rpc', ['cpp'],
    default_options : [
        'cpp_std=c++14',
        'cpp_eh=none'
    ],
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

incdir = include_directories('include')

if meson.get_compiler('cpp').get_id() == 'msvc'
    args += '/EHsc-'
endif

if host_machine.system() == 'windows'
    args += '/DDISCORD_WINDOWS'
    sources += [
        'src/connection_win.cpp',
        'src/discord_register_win.cpp'
    ]
    links += [
        'psapi.lib',
        'advapi.lib'
    ]
elif host_machine.system() == 'darwin'
    add_languages('objc')
    args += '-DDISCORD_OSX'
    sources += 'src/discord_register_osx.m'
    deps += dependency('appleframework', modules : 'AppKit')
else
    args += '-DDISCORD_LINUX'
    sources += 'src/discord_register_linux.cpp'
endif

json = subproject('rapidjson')

jsonincdir = json.get_variable('rapidjson_inc')

discord_lib = static_library('discord-rpc', sources, include_directories : [incdir, jsonincdir], cpp_args : args, install : true)
discord_dep = declare_dependency(link_with : discord_lib, include_directories : incdir)

pkg = import('pkgconfig')
pkg.generate(discord_lib, name : 'discord-rpc', description : 'Discord rich presence')