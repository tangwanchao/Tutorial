# 指定 cmake 最低要求版本
cmake_minimum_required(VERSION 3.10)

# 设置 c++ 标准
set(CMAKE_CXX_STANDARD 14)

# 设置项目名字
project(Tutorial VERSION 1.0)

# 提供用户可以选择的选项
option(USE_MYMATH "Use tutorial provided math implementation" ON)
# 配置文件,将版本号传递给源代码
configure_file(TutorialConfig.h.in TutorialConfig.h)

# 根据开关决定是否添加 MathFunctions 库
# 使用变量 EXTRA_LIBS 来收集所有可选库，以便以后链接到可执行文件中
# 变量 EXTRA_INCLUDES类似地用于可选的头文件
if(USE_MYMATH)
    add_subdirectory(MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
endif()

# 添加可执行文件
add_executable(Tutorial tutorial.cpp)

# 链接 MathFunctions 库
target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

# 指定编译目标(Turorial)时包含的路径
# 这样才能找到 .h(TutorialConfig.h) 文件
target_include_directories(Tutorial PUBLIC
        "${PROJECT_BINARY_DIR}"
        )