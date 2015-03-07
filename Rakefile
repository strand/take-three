desc "create a new note"
task :new_note do |task|
  Dir.mkdir "./notes" unless Dir.exists? "./notes"

  sh "touch #{generate_filepath}"
end

def generate_filepath
  if Dir["./notes/*"].last
    next_number = Dir["./notes/*"].map { |path| /(\d+)/.match(path)[1].to_i }
                                  .sort
                                  .last
                                  .next
    "notes/#{next_number}.md"
  else
    "notes/1.md"
  end
end

desc "generate the site"
task :generate_site do |task|
  Dir.mkdir "./site" unless Dir.exists? "./site"

  index_markdown = ""

  Dir["./notes/*"].each_with_index do |note_path, index|
    relative_path = "#{/(\d+)/.match(note_path)[1]}.html"
    html_path     = "./site/#{relative_path}"
    sh "pandoc #{note_path} -f markdown -t html -s -o #{html_path}"
    index_markdown << "- [note #{index + 1}](#{relative_path})\n"
  end

  File.open("./notes/index.md", "w") { |file| file << index_markdown }

  sh "pandoc ./notes/index.md -f markdown -t html -s -o ./site/index.html"

  sh "rm ./notes/index.md"
end
