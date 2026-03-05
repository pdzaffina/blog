---
layout: page
title: Prompts library
permalink: /prompts/
---

<style>
  /* Wrapper ensures the button is positioned relative to the prompt box */
  .prompt-wrapper {
    position: relative;
    margin-bottom: 20px;
  }

  /* Container for the rendered markdown prompt */
  .prompt-display {
    background-color: #f6f8fa;
    border: 1px solid #e1e4e8;
    border-radius: 6px;
    padding: 16px;
    padding-top: 40px; /* Extra space at top so copy button doesn't overlap first line */
    font-family: inherit;
    font-size: 0.95em;
    line-height: 1.6;
    overflow: auto;
  }

  /* Headings inside prompt content */
  .prompt-display h1,
  .prompt-display h2,
  .prompt-display h3,
  .prompt-display h4 {
    font-size: 1em;
    font-weight: 700;
    margin-top: 1.2em;
    margin-bottom: 0.4em;
  }

  .prompt-display h1 { font-size: 1.1em; }
  .prompt-display h2 { font-size: 1.05em; }

  /* Paragraphs */
  .prompt-display p {
    margin-top: 0;
    margin-bottom: 0.75em;
  }

  /* Inline code */
  .prompt-display code {
    background-color: #eaeef2;
    border-radius: 3px;
    font-family: SFMono-Regular, Consolas, "Liberation Mono", Menlo, monospace;
    font-size: 0.875em;
    padding: 0.15em 0.35em;
  }

  /* Fenced code blocks */
  .prompt-display pre {
    background-color: #1e1e2e;
    border-radius: 5px;
    color: #cdd6f4;
    font-family: SFMono-Regular, Consolas, "Liberation Mono", Menlo, monospace;
    font-size: 0.85em;
    line-height: 1.5;
    margin: 0.75em 0;
    overflow-x: auto;
    padding: 12px 16px;
  }

  /* Reset code inside pre so it doesn't double-style */
  .prompt-display pre code {
    background: none;
    border-radius: 0;
    color: inherit;
    font-size: inherit;
    padding: 0;
  }

  /* Lists */
  .prompt-display ul,
  .prompt-display ol {
    margin: 0.5em 0 0.75em 1.5em;
    padding: 0;
  }

  .prompt-display li {
    margin-bottom: 0.25em;
  }

  /* Blockquotes */
  .prompt-display blockquote {
    border-left: 3px solid #d1d5da;
    color: #6a737d;
    margin: 0.75em 0;
    padding: 0 1em;
  }

  /* Horizontal rules inside prompts */
  .prompt-display hr {
    border: none;
    border-top: 1px solid #e1e4e8;
    margin: 1em 0;
  }

  /* The Copy Button */
  .copy-btn {
    position: absolute;
    top: 8px;
    right: 8px;
    background-color: #fff;
    border: 1px solid #d1d5da;
    border-radius: 4px;
    color: #24292e;
    cursor: pointer;
    font-size: 12px;
    padding: 4px 8px;
    transition: background-color 0.2s;
    z-index: 1;
  }

  .copy-btn:hover {
    background-color: #f3f4f6;
  }

  /* Make the headings act like inline content so the arrow stays next to them */
  details summary h2, 
  details summary h3 {
    display: inline;
    margin: 0;
    padding: 0;
  }

  /* Indent titles */
  details.prompt-title {
    margin-left: 20px;
    margin-bottom: 10px;
  }
  
  summary {
    cursor: pointer;
    padding-top: 5px; 
    padding-bottom: 5px;
    margin-bottom: 10px;
  }

  /* Style for the credit line */
  .prompt-credit {
    font-size: 0.9em;
    font-style: italic;
    color: #555;
    margin-top: 0;
    margin-bottom: 10px;
    padding-left: 5px;
  }
</style>

{% assign all_prompts = site.prompts | where: "published", true %}
{% assign categories = all_prompts | map: 'category' | uniq | sort %}

{% for category in categories %}
  <details>
    <summary><h2>{{ category }}</h2></summary>
    
    {% assign category_prompts = all_prompts | where: "category", category %}
    
    {% for prompt in category_prompts %}
      <details class="prompt-title">
        <summary><h3>{{ prompt.title }}</h3></summary>
        
        {% if prompt.credit %}
          <div class="prompt-credit">Credit: {{ prompt.credit }}</div>
        {% endif %}

        <div class="prompt-wrapper">
          <button class="copy-btn" onclick="copyToClipboard(this)">Copy</button>
          <div class="prompt-display">
            {{ prompt.content | markdownify }}
          </div>
        </div>

      </details>
    {% endfor %}
    
  </details>
  <hr />
{% endfor %}

<script>
function copyToClipboard(button) {
  var wrapper = button.parentElement;
  var promptText = wrapper.querySelector('.prompt-display').innerText;

  navigator.clipboard.writeText(promptText).then(function() {
    var originalText = button.innerText;
    button.innerText = 'Copied!';
    setTimeout(function() {
      button.innerText = originalText;
    }, 2000);
  }, function(err) {
    console.error('Could not copy text: ', err);
  });
}
</script>
