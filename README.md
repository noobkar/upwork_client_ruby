# upwork_client_ruby
Ruby Task using Nokogiri
# Application Questions:
What is your favorite Ruby class/library or method and why?

Favorite Library: Nokogiri

Reason: Nokogiri is my go-to library for parsing and manipulating HTML and XML. Its intuitive syntax and powerful selectors make it incredibly efficient for web scraping tasks. I appreciate how it seamlessly integrates with Ruby, allowing for rapid development and easy maintenance of scraping scripts.

Given HTML: <div class="images"><img src="/pic.jpg"></div> Using Nokogiri how would you select the src attribute from the image? Show me two different ways to do that correctly with the HTML given.

Method 1: Using CSS Selectors

ruby
Copy code
require 'nokogiri'

html = '<div class="images"><img src="/pic.jpg"></div>'
doc = Nokogiri::HTML(html)
src = doc.css('div.images img').first['src']
puts src  # Output: /pic.jpg
Method 2: Using XPath


require 'nokogiri'

html = '<div class="images"><img src="/pic.jpg"></div>'
doc = Nokogiri::HTML(html)
src = doc.xpath('//div[@class="images"]/img').first['src']
puts src  # Output: /pic.jpg
If found HTML was a collection of li tags within a div with class="attr", how would you use Nokogiri to collect that information into one array?


require 'nokogiri'

html = <<-HTML
<div class="attr">
  <ul>
    <li>Attribute 1</li>
    <li>Attribute 2</li>
    <li>Attribute 3</li>
  </ul>
</div>
HTML

doc = Nokogiri::HTML(html)
attributes = doc.css('div.attr li').map(&:text)
puts attributes.inspect
# Output: ["Attribute 1", "Attribute 2", "Attribute 3"]
Given the following HTML:

<div class="listing">
  <div class="row">
    <span class="left">Title:</span>
    <span class="right">The Well-Grounded Rubyist</span>
  </div>
  <div class="row">
    <span class="left">Author:</span>
    <span class="right">David A. Black</span>
  </div>
  <div class="row">
    <span class="left">Price:</span>
    <span class="right">$34.99</span>
  </div>
  <div class="row">
    <span class="left">Description:</span>
    <span class="right">A great book for Rubyists</span>
  </div>
  <div class="row">
    <span class="left">Seller:</span>
    <span class="right">Ruby Scholar</span>
  </div>
</div>
Please collect all of the data presented into a key-value store. Please include code and the output.


require 'nokogiri'

html = <<-HTML
<div class="listing">
  <div class="row">
    <span class="left">Title:</span>
    <span class="right">The Well-Grounded Rubyist</span>
  </div>
  <div class="row">
    <span class="left">Author:</span>
    <span class="right">David A. Black</span>
  </div>
  <div class="row">
    <span class="left">Price:</span>
    <span class="right">$34.99</span>
  </div>
  <div class="row">
    <span class="left">Description:</span>
    <span class="right">A great book for Rubyists</span>
  </div>
  <div class="row">
    <span class="left">Seller:</span>
    <span class="right">Ruby Scholar</span>
  </div>
</div>
HTML

doc = Nokogiri::HTML(html)
data = {}

doc.css('div.listing div.row').each do |row|
  key = row.at_css('span.left').text.chomp(':').strip
  value = row.at_css('span.right').text.strip
  data[key] = value
end

puts data
Output:


{
  "Title" => "The Well-Grounded Rubyist",
  "Author" => "David A. Black",
  "Price" => "$34.99",
  "Description" => "A great book for Rubyists",
  "Seller" => "Ruby Scholar"
}
What Ruby feature do you hate?

While Ruby is a powerful and flexible language, I find that its global variables can sometimes lead to code that is hard to debug and maintain. The use of global variables can create unintended side effects, making it challenging to track the flow of data within an application. However, with disciplined coding practices and proper scoping, this issue can be mitigated.
