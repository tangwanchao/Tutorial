# 添加 MathFunctions 为库
add_library(MathFunctions mysqrt.cpp)

# 指出与我们链接的任何人都需要包含当前源目录
# INTERFACE 是指消费者需要的东西
target_include_directories(MathFunctions
        INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
        )