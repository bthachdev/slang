# Slang

Very much inspired by [slim](https://github.com/slim-template/slim), this is a templating language which converts to ECR (embedded crystal) and then to HTML.

## Status

**ALPHA** -> No tests, no real-world usage, just playing with creating a nice parser/lexer that gives us slim-like templating capabilities.

## Installation

Add this to your application's `shard.yml`:

```yaml
dependencies:
  slang:
    github: jeromegn/slang
```

## Usage

### Render a file

```crystal
String.build do |str|
  embed_slang("path/to/file.slang", "str")
end
```

## Syntax

```slim
span#some-id.classname
  #hello.world.world2
    span data-some-var=some_var
      span
        span.deep_nested
          = Process.pid
          | text node
          ' other text node syntax
    span.alongside pid=Process.pid
      custom-tag#with-id pid="#{Process.pid}"
        - strings.each do |s|
          span
            = s
#amazing-div some-attr="hello"
```

compiles to ECR:

```html
<span id="some-id" class="classname">
  <div id="hello" class="world world2">
    <span data-some-var="<%= some_var %>">
      <span>
        <span class="deep_nested">
          <%= Process.pid %>
          <%= "text node" %>
          <%= "other text node syntax" %>
        </span>
      </span>
    </span>
    <span class="alongside" pid="<%= Process.pid %>">
      <custom-tag id="with-id" pid="<%= "#{Process.pid}" %>">
        <% strings.each do |s| %>
          <span>
            <%= s %>
          </span>
        <% end %>
      </custom-tag>
    </span>
  </div>
</span>
<div id="amazing-div" some-attr="<%= "hello" %>"></div>
```

## Roadmap

- [ ] Documentation
- [ ] No need to rely on ECR probably, but that's optimization at this point
- [ ] Support "inline"
- [ ] More robust lexer for detecting start and end of code to evaluate (well, for ECR to evaluate)

## Contributing

1. Fork it ( https://github.com/jeromegn/slang/fork )
2. Create your feature branch (git checkout -b my-new-feature)
3. Commit your changes (git commit -am 'Add some feature')
4. Push to the branch (git push origin my-new-feature)
5. Create a new Pull Request

## Contributors

- [jeromegn](https://github.com/jeromegn) Jerome Gravel-Niquet - creator, maintainer