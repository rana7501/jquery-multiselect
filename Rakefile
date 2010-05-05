require 'rubygems'
require 'bundler'

Bundler.setup
Bundler.require

desc "Compile CoffeeScripts and watch for changes"
task :coffee do
  coffee = IO.popen 'coffee -wc --no-wrap src/*.coffee -o js 2>&1'
  
  while line = coffee.gets
    puts line
  end
end

desc "Build minified version"
task :build do
  content = File.read("js/jquery.multiselect.js")
  minyfied = JSMin.minify(content)
  version = File.read("VERSION")
  
  licence = <<LIC
/**
 * Copyright (c) 2010 Wilker Lúcio
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *    http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
LIC
  
  File.open("dist/jquery.multiselect.#{version}.min.js", "wb") do |f|
    f << licence
    f << minyfied
  end
end