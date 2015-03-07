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

  Dir["./notes/*"].each do |note_path|
    html_path = "./site/#{/(\d+)/.match(note_path)[1]}.html"
    sh "pandoc #{note_path} -f markdown -t html -s -o #{html_path}"
  end
end
