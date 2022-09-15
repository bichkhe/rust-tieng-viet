  {% for k1,v1 in page %}
                    {{k1}} - {{v1}}
                    {% endfor %}


                    {% set_global all_pages = [] %}
                    {% set_global found = true %}
                    {% set categories = get_taxonomy(kind="tags") %}
                    {% set_global total_pages = 0 %}
                    {% for k, v in categories %}
                    {% if k == 'items' %}
                    {% for term in v %}
                    {% set len = term.pages | length %}
                    {% set_global total_pages = total_pages + len %}
                    {% if total_pages > 0 %}
                    {% for page in term.pages %}
                    {% for p in all_pages %}
                    <!-- {% if p.permalink == page.permalink %}
                    {% set_global found = true %}
                    {% endif %} -->
                    {% endfor %}

                    <!-- {{all_pages}} -->
                    <!-- {{page.title}} -- {{term.name}} -->

                    {% endfor %}
                    {% if found == true %}
                    {% set_global all_pages = all_pages | concat(with=page) %}
                    {% endif %}
                    {%endif%}
                    {% endfor %}
                    {%endif%}
                    {% endfor %}
                    {% for page in all_pages %}
                    <li>
                        <span>
                            <h6 class="font-weight-bold">
                                <a href="{{page.permalink}}" class="text-dark">{{page.title}}</a>
                            </h6>
                            <p class="text-muted">
                                {{page.date | date}}
                            </p>
                        </span>
                    </li>
                    {% endfor %}