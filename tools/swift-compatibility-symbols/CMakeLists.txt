add_swift_host_tool(swift-compatibility-symbols
  swift-compatibility-symbols.cpp
  LLVM_LINK_COMPONENTS support
  SWIFT_COMPONENT tools
)

set(syms_file "${CMAKE_BINARY_DIR}/share/swift/compatibility-symbols")

add_custom_command_target(copy_compat_target
  OUTPUT
    ${syms_file}
  COMMAND
    "${SWIFT_NATIVE_SWIFT_TOOLS_PATH}/swift-compatibility-symbols"
      --output-filename ${syms_file}
  DEPENDS
    swift-compatibility-symbols
)

add_dependencies(swift-frontend "${copy_compat_target}")

swift_install_in_component(
  FILES
    ${syms_file}
  DESTINATION
    "share/swift"
  COMPONENT
    compiler
)
