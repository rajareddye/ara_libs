cmake_minimum_required(VERSION 3.14)
project(arxml)

add_library(
  arxml SHARED
  pugiconfig.hpp pugixml.hpp pugixml.cpp arxml_node.h arxml_node.cpp arxml_node_iterator.h arxml_node_range.h arxml_reader.h arxml_reader.cpp
)
