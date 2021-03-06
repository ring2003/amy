import os
import platform

system = platform.system()
libpath = [Dir('/usr/lib'), Dir('/usr/local/lib')] +\
          [Dir('/usr/local/lib/mysql')] if system == 'FreeBSD' else []

env = Environment(ENV=os.environ,
                  CXX=os.environ.get('CXX', 'clang++'),
                  CCFLAGS='-ggdb -std=c++11',
                  CPPPATH=[Dir('include'),
                           Dir('/usr/local/include')],
                  CPPDEFINES=[('BOOST_PARAMETER_MAX_ARITY', 6)],
                  LIBPATH=libpath)

libs = ['boost_system',
        'boost_thread-mt' if system == 'Darwin' else 'boost_thread',
        'mysqlclient',
        'pthread']

env.Execute('@doxygen Doxyfile')

env.SConscript(dirs=['test'],
               exports=['env', 'libs'],
               variant_dir='build/test',
               duplicate=0)

env.SConscript(dirs=['example'],
               exports=['env', 'libs'],
               variant_dir='build/example',
               duplicate=0)

# vim:ft=python ts=4 sw=4 et
