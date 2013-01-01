# encoding: UTF-8
require 'cgi'

desc 'Convert to Jekyll source'
task :default do

  # YAML Front Matter
  jekyllHead = <<-EOS
---
title: %title%
repository: %repository%
branch: '%branch%'
layout: default
---

  EOS

  Dir['./_repos/*/*'].each do |repoDir|
    # ./_repos/:repository/:brach -> _posts/:repository/:branch
    docsOut = repoDir.gsub /\/_repos/, ''
    # _repos/:repository/:brach/docs
    docsIn  = repoDir + '/docs'
    # _posts/:repository/:branch -> [:branch, :repository, '_posts']
    branchName, repoName = docsOut.split('/').reverse()

    FileUtils.mkdir_p(docsOut)

    Dir[docsIn+'/*'].each do |srcPath|
      baseName = File.basename(srcPath)
      destPath = docsOut + '/' + baseName

      if File.extname(srcPath) == '.md'
        content = File.read(srcPath)

        # http://mattn.kaoriya.net/software/lang/ruby/20121011184445.htm
        content.gsub!(/(?:^|\n)```(\w*)\n(.*?\n)```\n/m) do |text|
          cls = $1.empty? ? "" : "#{$1}"
          "\n<pre class=\"#{cls}\"><code>#{CGI.escapeHTML($2)}</code></pre>\n"
        end

        fp = File.open(destPath, 'w')
        fp.write(jekyllHead.gsub(/%title%/, baseName).gsub(/%repository%/, repoName).gsub(/%branch%/, branchName) + content)
        fp.close()
      else
        FileUtils.cp(srcPath, destPath)
      end
    end
  end
end