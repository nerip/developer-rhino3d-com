---
layout: fullwidth-page
title: Administration
permalink: /admin/
order: 1
---

# Administration

The goal of this site is to consolidate all the (now) scattered developer documentation into a single canonical site that is clear, easy-to-navigate, with consistent formatting and nomenclature.

The sources of content-to-be-consolidated are:

- <strike>Rhino Developer wiki</strike>
- [RhinoCommon API references](http://4.rhino3d.com/5/rhinocommon/)...underway
- [C++ SDK API references](http://4.rhino3d.com/5/rhinocppsdk/idx.html)
- <strike>RhinoCommon samples on GitHub</strike>
- [DaleF's CsCommands](https://github.com/dalefugier/SampleCsCommands/)
- [Doxygen Docs (on McNeel intranet)](http://phab.mcneel.com/docs/rhino/6/rhinocommon/)
- Dale Lear's Developer Meeting Notes
- RhinoScript and Rhino.Python Primers
- Mitch's MicMac tools: http://wiki.mcneel.com/people/mitchheynick
- [Grasshopper SDK Help file (chm)](http://s3.amazonaws.com/files.na.mcneel.com/grasshopper/1.0/docs/en/GrasshopperSDK.chm).
- Grasshopper posts ([How and Why of Datatrees](http://www.grasshopper3d.com/forum/topics/the-why-and-how-of-data-trees)), etc.
- Macros documentation sources: [Macros in Helpfile](http://docs.mcneel.com/rhino/5/help/en-us/information/rhinoscripting.htm), [Macros in Wiki](http://wiki.mcneel.com/rhino/basicmacros), [Using the MacroEditor](http://wiki.mcneel.com/developer/macroscriptsetup)

**DO NOT** port any content that relates to pre-Rhino 5: this is old information.  Visual Studio 2010 for the C/C++ SDK was used for Rhino 5.

---

## Dev Docs Guides

- [Getting Started with Developer Docs](https://github.com/mcneel/developer-rhino3d-com/blob/master/README.md)
- [How This Site Works]({{ site.baseurl }}/guides/general/how_this_site_works)
- [Developer Docs Style Guide]({{ site.baseurl }}/guides/general/developer_docs_style_guide)

---

## TODO List

### Guides

The following guides have TODO items:

{% assign guides = site.guide_topics | sort:"title" | sort:"apis" %}
<div class="trigger">
  <ol>
  {% for topic in guides %}
    {% if topic.TODO %}
      <li>
        ({{ topic.apis }}) <a class="page-link" href="{{ topic.url | prepend: site.baseurl }}">{{ topic.title }}</a> {{ topic.TODO }} {% if topic.origin != 'unset' and topic.TODO == 'needs porting' %} from: <a href="{{ topic.origin }}">{{ topic.origin }}</a>{% endif %}
      </li>
    {% endif %}
  {% endfor %}
  </ol>
</div>

### Samples

The following samples have TODO items:

{% assign samples = site.samples | sort:"title" | sort:"apis" %}
<div class="trigger">
  <ol>
  {% for sample in samples %}
    {% if sample.TODO %}
      <li>
        ({{ sample.apis }}) <a class="page-link" href="{{ sample.url | prepend: site.baseurl }}">{{ sample.title }}</a>  {{ sample.TODO }} {% if sample.origin != 'unset'  and sample.TODO == 'needs porting' %} from: <a href="{{ sample.origin }}">{{ sample.origin }}</a>{% endif %}
    </li>
    {% endif %}
  {% endfor %}
  </ol>
</div>

### Misc

See [YouTrack: project: WWW subsystem: developer.rhino3d.com #unresolved](http://mcneel.myjetbrains.com/youtrack/issues?q=project%3A+WWW+subsystem%3A+developer.rhino3d.com+%23unresolved)
