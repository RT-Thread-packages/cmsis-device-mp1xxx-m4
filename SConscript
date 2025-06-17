from building import *
import os

# Import environment variables
Import('env')

# Get the current working directory
cwd = GetCurrentDir()

# Initialize include paths and source files list
path = [os.path.join(cwd, 'Include')]
src = [os.path.join(cwd, 'Source', 'Templates', 'system_stm32mp1xx.c')]

# Map microcontroller units (MCUs) to their corresponding startup files
mcu_startup_files = {
    'STM32MP15xx': 'startup_stm32mp15xx.s',
    'STM32MP157Axx': 'startup_stm32mp15xx.s',
    'STM32MP157Cxx': 'startup_stm32mp15xx.s',
    'STM32MP153Axx': 'startup_stm32mp15xx.s',
    'STM32MP153Cxx': 'startup_stm32mp15xx.s',
    'STM32MP151Axx': 'startup_stm32mp15xx.s',
    'STM32MP151Cxx': 'startup_stm32mp15xx.s',
}

# Check each defined MCU, match the platform and append the appropriate startup file
cpp_defines_tuple = env.get('CPPDEFINES', [])
cpp_defines_list = [item[0] if isinstance(item, tuple) else item for item in cpp_defines_tuple]
for mcu, startup_file in mcu_startup_files.items():
    if mcu in cpp_defines_list:
        if rtconfig.PLATFORM in ['gcc', 'llvm-arm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'gcc', startup_file)]
        elif rtconfig.PLATFORM in ['armcc', 'armclang']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'arm', startup_file)]
        elif rtconfig.PLATFORM in ['iccarm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'iar', startup_file)]
        break

# Define the build group
group = DefineGroup('STM32MP-CMSIS', src, depend=['PKG_USING_STM32MP1_M4_CMSIS_DRIVER'], CPPPATH=path)

# Return the build group
Return('group')
