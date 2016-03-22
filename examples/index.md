---
layout: page
title: Examples
excerpt: "Examples showing how to use metaknowledge to analyze data."
search_omit: true
---

<ul class="post-list">

  <li><article>
  <a href="{{ site.baseurl }}/examples/#Context">Context</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Importing">Importing</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Reading-Files">Reading Files</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Record-object">Record object</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#RecordCollection-object">RecordCollection object</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Citation-object">Citation object</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Filtering">Filtering</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Exporting-RecordCollections">Exporting RecordCollections</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-co-citation-network">Making a co-citation network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-citation-network">Making a citation network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-co-author-network">Making a co-author network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-one-mode-network">Making a one-mode network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-two-mode-network">Making a two-mode network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Making-a-multi-mode-network">Making a multi-mode network</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Post-processing-graphs">Post processing graphs</a>
  </article></li>
  <li><article>
  <a href="{{ site.baseurl }}/examples/#Exporting-graphs">Exporting graphs</a>
  </article></li>
</ul>

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Context">Context<a class="anchor-link" href="#Context">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>{% comment %}</p>
<h1 id="Notes-for-those-who-downloaded-the-notebook">Notes for those who downloaded the notebook<a class="anchor-link" href="#Notes-for-those-who-downloaded-the-notebook">&#182;</a></h1><p>The notebook should just work as long as you put the sample file (<code>savedrecs.txt</code>) in the same directory as this file.</p>
<p>The one issue you will have is that the urls will not work. To make them work you will need to replace <code>{{ site.baseurl }}</code> with <code>http://networkslab.org/metaknowledge</code>, sorry about that.</p>
<p>{% endcomment %}</p>
<p><em>metaknowledge</em> is a python library for creating and analyzing scientific metadata. It uses records obtained from Web of Science (WOS) and mostly produces graphs. As it is intended to be usable by those who do not know much python. This page will be a short overview of its capabilities, to allow you to use it for your own work. For complete coverage of the package as well as install instructions read the full the documentation <a href="{{ site.baseurl }}/documentation">here</a>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>This document was made from a <a href="https://jupyter.org">jupyter</a> notebook, if you know how to use them, you can download the notebook <a href="{{ site.baseurl }}/examples/metaknowledgeExamples.ipynb">here</a> and the sample file is <a href="{{ site.baseurl }}/examples/savedrecs.txt">here</a> if you wish to have an interactive version of this page. Now lets begin.</p>
<h1 id="Importing">Importing<a class="anchor-link" href="#Importing">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>First you need to import the <em>metaknowledge</em> package</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">metaknowledge</span> <span class="k">as</span> <span class="nn">mk</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>And you will often need the <a href="https://networkx.github.io/documentation/networkx-1.9.1/"><em>networkx</em></a> package</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">networkx</span> <span class="k">as</span> <span class="nn">nx</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>I am using <a href="http://matplotlib.org/"><em>matplotlib</em></a> to display the graphs and to make them look nice when displayed</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><em>metaknowledge</em> also has a <em>matplotlib</em> based graph <a href="{{ site.baseurl }}/documentation/metaknowledgeFull.html#contour">visualizer</a> that we will use, the module also contains the titular contour plot generator</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">metaknowledge.contour</span> <span class="k">as</span> <span class="nn">mkv</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The functions for handling the raw WOS tags are all found in <a href="{{ site.baseurl }}/documentation/metaknowledgeFull.html#tagProcessing"><em>tagProcessing</em></a> which also contains low level interface to them</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">metaknowledge.tagProcessing</span> <span class="k">as</span> <span class="nn">mkt</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="http://pandas.pydata.org/"><em>pandas</em></a> is also used in one example</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="kn">import</span> <span class="nn">pandas</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Reading-Files">Reading Files<a class="anchor-link" href="#Reading-Files">&#182;</a></h1><p>The files from the Web of Science (WOS) can be loaded into a <a href="{{ site.baseurl }}/docs/RecordCollection#RecordCollection"><code>RecordCollections</code></a> by creating a <code>RecordCollection</code> with the path to the files given to it as a string.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">RecordCollection</span><span class="p">(</span><span class="s">&quot;savedrecs.txt&quot;</span><span class="p">)</span>
<span class="nb">repr</span><span class="p">(</span><span class="n">RC</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[7]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;savedrecs&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>You can also read a whole directory, in this case it is reading the current working directory</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">RecordCollection</span><span class="p">(</span><span class="s">&quot;.&quot;</span><span class="p">)</span>
<span class="nb">repr</span><span class="p">(</span><span class="n">RC</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[8]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;files-from-.&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><em>metaknowledge</em> can detect if a file is a valid WOS file or not and will read the entire directory and load only those that have the right header. You can also tell it to only read a certain type of file, by using the extension argument.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">RecordCollection</span><span class="p">(</span><span class="s">&quot;.&quot;</span><span class="p">,</span> <span class="n">extension</span> <span class="o">=</span> <span class="s">&quot;txt&quot;</span><span class="p">)</span>
<span class="nb">repr</span><span class="p">(</span><span class="n">RC</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[9]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;txt-files-from-.&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now you have a <code>RecordCollection</code> composed of all the WOS records in the selected file(s).</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="s">&quot;RC is a &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">RC</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>RC is a Collection of 32 records
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>You might have noticed I used two different ways to display the <code>RecordCollection</code>. <code>repr(RC)</code> will give you where <em>metaknowledge</em> thinks the collection came from. While <code>str(RC)</code> will give you a nice string containing the number of <code>Records</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Record-object"><code>Record</code> object<a class="anchor-link" href="#Record-object">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/Record#Record"><code>Record</code></a> is an object that contains a simple WOS record, for example a journal article, book, or conference proceedings. They are what <a href="{{ site.baseurl }}/docs/RecordCollection#RecordCollection"><code>RecordCollections</code></a> contain. To see an individual <a href="{{ site.baseurl }}/docs/Record#Record"><code>Record</code></a> at random from a <code>RecordCollection</code> you can use <code>peak()</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">R</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">peak</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>A single <code>Record</code> can give you all the information it contains about its record. If for example you want its authors.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="o">.</span><span class="n">authorsFull</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="o">.</span><span class="n">AF</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[&apos;HUGONIN, JP&apos;, &apos;PETIT, R&apos;]
[&apos;HUGONIN, JP&apos;, &apos;PETIT, R&apos;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Converting a <code>Record</code> to a string will give its title</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>GENERAL STUDY OF DISPLACEMENTS AT TOTAL REFLECTION
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>If you try to access a tag the <code>Record</code> does not have it will return <code>None</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="o">.</span><span class="n">GP</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>None
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>There are two ways of getting each tag, one is using the WOS 2 letter abbreviation and the second is to use the human readable name. There is no standard for the human readable names, so they are specific to <em>metaknowledge</em>. To see how the WOS names map to the long names look at <a href="{{ site.baseurl }}/docs/tagFuncs#tagFuncs">tagFuncs</a>. If you want all the tags a <code>Record</code> has use <a href="({{ site.baseurl }}/docs/Record#activeTags"><code>activeTags()</code></a>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="o">.</span><span class="n">activeTags</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[&apos;PT&apos;, &apos;AU&apos;, &apos;AF&apos;, &apos;TI&apos;, &apos;SO&apos;, &apos;LA&apos;, &apos;DT&apos;, &apos;C1&apos;, &apos;CR&apos;, &apos;NR&apos;, &apos;TC&apos;, &apos;Z9&apos;, &apos;PU&apos;, &apos;PI&apos;, &apos;PA&apos;, &apos;SN&apos;, &apos;J9&apos;, &apos;JI&apos;, &apos;PY&apos;, &apos;VL&apos;, &apos;IS&apos;, &apos;BP&apos;, &apos;EP&apos;, &apos;DI&apos;, &apos;PG&apos;, &apos;WC&apos;, &apos;SC&apos;, &apos;GA&apos;, &apos;UT&apos;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="RecordCollection-object"><code>RecordCollection</code> object<a class="anchor-link" href="#RecordCollection-object">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/RecordCollection#RecordCollection"><code>RecordCollection</code></a> is the object that <em>metaknowledge</em> uses the most. It is your interface with the data you want.</p>
<p>To iterate over all of the <code>Records</code> you can use a for loop</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="k">for</span> <span class="n">R</span> <span class="ow">in</span> <span class="n">RC</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">R</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>GENERAL STUDY OF DISPLACEMENTS AT TOTAL REFLECTION
EXCHANGED MOMENTUM BETWEEN MOVING ATOMS AND A SURFACE-WAVE - THEORY AND EXPERIMENT
SPIN ANGULAR-MOMENTUM OF A FIELD INTERACTING WITH A PLANE INTERFACE
SPIN ANGULAR-MOMENTUM OF A FIELD INTERACTING WITH A PLANE INTERFACE
NONLINEAR TOTALLY REFLECTING PRISM COUPLER - THERMOMECHANIC EFFECTS AND INTENSITY-DEPENDENT REFRACTIVE-INDEX OF THIN-FILMS
Longitudinal and transverse effects of nonspecular reflection
Experimental observation of the Imbert-Fedorov transverse displacement after a single total reflection
SHIFTS OF COHERENT-LIGHT BEAMS ON REFLECTION AT PLANE INTERFACES BETWEEN ISOTROPIC MEDIA
Goos-Hanchen shift as a probe in evanescent slab waveguide sensors
DISCUSSIONS OF PROBLEM OF PONDEROMOTIVE FORCES
MECHANICAL INTERPRETATION OF SHIFTS IN TOTAL REFLECTION OF SPINNING PARTICLES
RESONANCE EFFECTS ON TOTAL INTERNAL-REFLECTION AND LATERAL (GOOS-HANCHEN) BEAM DISPLACEMENT AT THE INTERFACE BETWEEN NONLOCAL AND LOCAL DIELECTRIC
THEORETICAL NOTES ON AMPLIFICATION OF TRANSVERSE SHIFT BY TOTAL REFLECTION ON MULTILAYERED SYSTEM
INTERFERENCE THEORY OF REFLECTION FROM MULTILAYERED MEDIA
EXPERIMENTS IN PHENOMENOLOGICAL ELECTRODYNAMICS AND THE ELECTROMAGNETIC ENERGY-MOMENTUM TENSOR
CALCULATION AND MEASUREMENT OF FORCES AND TORQUES APPLIED TO UNIAXIAL CRYSTAL BY EXTRAORDINARY WAVE
TRANSVERSE DISPLACEMENT OF A TOTALLY REFLECTED LIGHT-BEAM AND PHASE-SHIFT METHOD
ANGULAR SPECTRUM AS AN ELECTRICAL NETWORK
Transverse displacement at total reflection near the grazing angle: a way to discriminate between theories
Simple technique for measuring the Goos-Hanchen effect with polarization modulation and a position-sensitive detector
Goos-Hanchen and Imbert-Fedorov shifts for leaky guided modes
OBSERVATION OF SHIFTS IN TOTAL REFLECTION OF A LIGHT-BEAM BY A MULTILAYERED STRUCTURE
INTERNAL PHOTON IMPULSE OF DIELECTRIC AND ON COUPLE APPLIED TO ANISOTROPIC CRYSTAL
LONGITUDINAL AND TRANSVERSE DISPLACEMENTS OF A BOUNDED MICROWAVE BEAM AT TOTAL INTERNAL-REFLECTION
Numerical study of the displacement of a three-dimensional Gaussian beam transmitted at total internal reflection. Near-field applications
A Novel Method for Enhancing Goos-Hanchen Shift in Total Internal Reflection
PREDICTION OF A RESONANCE-ENHANCED LASER-BEAM DISPLACEMENT AT TOTAL INTERNAL-REFLECTION IN SEMICONDUCTORS
ASYMMETRICAL MOMENTUM-ENERGY TENSORS AND 6-COMPONENT ANGULAR-MOMENTUM IN PROBLEM CONCERNING 2 PHOTON MOMENTA AND MAGNETODYNAMIC EFFECT PROBLEM
WHY ENERGY FLUX AND ABRAHAMS PHOTON MOMENTUM ARE MACROSCOPICALLY SUBSTITUTED FOR MOMENTUM DENSITY AND MINKOWSKIS PHOTON MOMENTUM
Optical properties of nanostructured thin films
DISPLACEMENT OF A TOTALLY REFLECTED LIGHT-BEAM - FILTERING OF POLARIZATION STATES AND AMPLIFICATION
CONSERVATION OF ANGULAR MOMENT WITH SIX COMPONENTS AND ASYMMETRICAL IMPULSE ENERGY TENSORS
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The individual <code>Records</code> are index by their WOS numbers so you can access a specific one in the collection if you know its number.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC</span><span class="o">.</span><span class="n">WOS</span><span class="p">(</span><span class="s">&quot;WOS:A1979GV55600001&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[17]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt; metaknowledge.record.Record object WOS:A1979GV55600001 &gt;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Citation-object"><code>Citation</code> object<a class="anchor-link" href="#Citation-object">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/Citation#Citation"><code>Citation</code></a> is an object to contain the results of parsing a citation. They can be created from a <code>Record</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">Cite</span> <span class="o">=</span> <span class="n">R</span><span class="o">.</span><span class="n">createCitation</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="n">Cite</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>COSTADEB.O, 1974, CR ACAD SCI A MATH, V279, P123
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><code>Citations</code> allow for the raw strings of citations to be manipulated easily by <em>metaknowledge</em>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Filtering">Filtering<a class="anchor-link" href="#Filtering">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The for loop shown above is the main way to filter a RecordCollection, that said there are a few builtin filters, e.g. <a href="{{ site.baseurl }}/docs/RecordCollection#yearSplit"><code>yearSplit()</code></a>, but the for loop is an easily generalized way of filtering that is relatively simple to read so it the main way you should filter. An example of the workflow is as follows:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>First create a new RecordCollection</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RCfiltered</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">RecordCollection</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Then add the records that meet your condition, in this case that their title's start with <code>'A'</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="k">for</span> <span class="n">R</span> <span class="ow">in</span> <span class="n">RC</span><span class="p">:</span>
    <span class="k">if</span> <span class="n">R</span><span class="o">.</span><span class="n">title</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">==</span> <span class="s">&#39;A&#39;</span><span class="p">:</span>
        <span class="n">RCfiltered</span><span class="o">.</span><span class="n">addRec</span><span class="p">(</span><span class="n">R</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="nb">print</span><span class="p">(</span><span class="n">RCfiltered</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Collection of 3 records
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now you have a RecordCollection <code>RCfiltered</code> of all the <code>Records</code> whose titles begin with <code>'A'</code>.</p>
<p>One note about implementing this, the above code does not handle the case in which the title is missing i.e. <code>R.title</code> is <code>None</code>. You will have to deal with this on your own.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Two builtin functions to filter collections are <a href="{{ site.baseurl }}/docs/RecordCollection#yearSplit"><code>yearSplit()</code></a> and <a href="{{ site.baseurl }}/docs/RecordCollection#localCitesOf"><code>localCitesOf()</code></a>. To get a RecordCollection of all Records between 1970 and 1979:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RC70</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">yearSplit</span><span class="p">(</span><span class="mi">1970</span><span class="p">,</span> <span class="mi">1979</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">RC70</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Collection of 19 records
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The second function <a href="{{ site.baseurl }}/docs/RecordCollection#localCitesOf"><code>localCitesOf()</code></a> takes in an object that a <a href="{{ site.baseurl }}/docs/Citation#Citation">Citation</a> can be created from and returns a RecordCollection of all the Records that cite it. So to see all the records that cite <code>"Yariv A., 1971, INTRO OPTICAL ELECTR"</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[23]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RCintroOpt</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">localCitesOf</span><span class="p">(</span><span class="s">&quot;Yariv A., 1971, INTRO OPTICAL ELECTR&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">RCintroOpt</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Collection of 1 records
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Exporting-RecordCollections">Exporting RecordCollections<a class="anchor-link" href="#Exporting-RecordCollections">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now you have a filtered RecordCollection you can write it as a file with <a href="{{ site.baseurl }}/docs/RecordCollection#writeFile"><code>writeFile()</code></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre> <span class="n">RCfiltered</span><span class="o">.</span><span class="n">writeFile</span><span class="p">(</span><span class="s">&quot;Records_Starting_with_A.txt&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The written file is identical to one of those produced by WOS.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>If you wish to have a more useful file use <a href="{{ site.baseurl }}/docs/RecordCollection#writeCSV"><code>writeCSV()</code></a> which creates a CSV file of all the tags as columns and the Records as rows. IF you only care about a few tags the <code>onlyTheseTags</code> argument allows you to control the tags.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[25]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">selectedTags</span> <span class="o">=</span> <span class="p">[</span><span class="s">&#39;TI&#39;</span><span class="p">,</span> <span class="s">&#39;UT&#39;</span><span class="p">,</span> <span class="s">&#39;CR&#39;</span><span class="p">,</span> <span class="s">&#39;AF&#39;</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>This will give only the title, WOS number, citations, and authors.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">RCfiltered</span><span class="o">.</span><span class="n">writeCSV</span><span class="p">(</span><span class="s">&quot;Records_Starting_with_A.csv&quot;</span><span class="p">,</span> <span class="n">onlyTheseTags</span> <span class="o">=</span> <span class="n">selectedTags</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The last export feature is for using <em>metaknowledge</em> with other packages, in particular <a href="http://pandas.pydata.org/"><em>pandas</em></a> but others should also work. <a href="{{ site.baseurl }}/docs/RecordCollection#makeDict"><code>makeDict()</code></a> creates a dictionary with tags as keys and lists as values with each index of the lists corresponding to a Record. <em>pandas</em> can accept these directly to make DataFrames.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">recDataFrame</span> <span class="o">=</span> <span class="n">pandas</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">RC</span><span class="o">.</span><span class="n">makeDict</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-co-citation-network">Making a co-citation network<a class="anchor-link" href="#Making-a-co-citation-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>To make a basic co-citation network of Records use <a href="{{ site.baseurl }}/docs/RecordCollection#coCiteNetwork"><code>coCiteNetwork()</code></a>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coCites</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">coCiteNetwork</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">coCites</span><span class="p">,</span> <span class="n">makeString</span> <span class="o">=</span> <span class="k">True</span><span class="p">))</span> <span class="c">#makestring by default is True so it is not strictly necessary to include</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 570 nodes, 17620 edges, 0 isolates, 26 self loops, a density of 0.108655 and a transitivity of 0.68445
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/documentation/metaknowledgeFull.html#graphStats"><code>graphStats()</code></a> is a function to extract some of the statists of a graph and make them into a nice string.</p>
<p><code>coCites</code> is now a <a href="https://networkx.github.io/documentation/networkx-1.9.1/"><em>networkx</em></a> graph of the co-citation network, with the hashes of the <code>Citations</code> as nodes and the full citations stored  as an attributes. Lets look at one node</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coCites</span><span class="o">.</span><span class="n">nodes</span><span class="p">(</span><span class="n">data</span> <span class="o">=</span> <span class="k">True</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[29]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>(&apos;Hodgkinson Ij, 1988, CRIT REV SOLID STATE&apos;,
 {&apos;count&apos;: 1, &apos;info&apos;: &apos;Hodgkinson Ij, 1988, CRIT REV SOLID STATE, V15, P27&apos;})</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>and an edge</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coCites</span><span class="o">.</span><span class="n">edges</span><span class="p">(</span><span class="n">data</span> <span class="o">=</span> <span class="k">True</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[30]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>(&apos;Hodgkinson Ij, 1988, CRIT REV SOLID STATE&apos;,
 &apos;Lalanne P, 1996, J MOD OPTIC&apos;,
 {&apos;weight&apos;: 1})</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>All the graphs <em>metaknowledge</em> use are <em>networkx</em> graphs, a few functions to trim them are implemented in <em>metaknowledge</em>, <a href="#filtering-graphs">here</a> is the example section, but many useful functions are implemented by it. Read the documentation <a href="https://networkx.github.io/documentation/networkx-1.9.1/">here</a> for more information.</p>
<p>The <code>coCiteNetwork()</code> function has many options for filtering and determining the nodes. The default is to use the <code>Citations</code> themselves. If you wanted to make a network of co-citations of journals you would have to make the node type <code>'journal'</code> and remove the non-journals.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coCiteJournals</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">coCiteNetwork</span><span class="p">(</span><span class="n">nodeType</span> <span class="o">=</span> <span class="s">&#39;journal&#39;</span><span class="p">,</span> <span class="n">dropNonJournals</span> <span class="o">=</span> <span class="k">True</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">coCiteJournals</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 90 nodes, 1411 edges, 0 isolates, 41 self loops, a density of 0.35231 and a transitivity of 0.636776
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Lets take a look at the graph after a quick spring layout</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[32]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">nx</span><span class="o">.</span><span class="n">draw_spring</span><span class="p">(</span><span class="n">coCiteJournals</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
B+F3feHNvn37oNFo8NlnnyE5ORlHjhy57pjS0lJkZGSgqKgI77zzDoCems/Hjh0L+XqRznTYjUZ4
PB5MnjwZs2bNQmJiIoqLi7Fo0SLMmzcPo0aNQlJSEubNm4ctW7b0W77yVlwgR0OXAgADfd+ZBrdd
O3fK4oULZbzfL5Xt7TJbRHqXxvikZ3HVBqtVPlYUWVdbKw+Xl4d0/tbWVrl48aKIiDgcDi6EuSYl
JUVycnIkOztb/H6/rFq1qs/jS5Yske3bt8vtt98uy5cvl5KSErFarXL69GlJSEgI6Vo7duyQTQsW
yP729rBea6GiyDGrVVwul3i9XmlubpZz585JcXGx3H333TJt2jTJzMwURVFuep5dO3fKsscek3c7
OmRkkNc+JSJTzWZZvWlTyJ89orANdPrT0DDQI9WhaNu2bdBqtTh06BCSkpKua8338ssvw2Qy4Z57
7sGf/vSnQIejcEo7RmMfdoKi4Ac/+AGee+45vPfee/22EgzGrbZAjoYmjnxJdRypqgOAOJ1O+dGP
fiSffPKJPPvss/LDH/4w8Phbb70lJSUlMnv2bHn00Udl/PjxMmvWLPnPf/4T0nVaW1vF63ZLi88n
4W728YmIXa+X083NUfk8xHq2hShS3OdLquNeSXUoiiI/+9nPZMeOHVJRUXHdnt/U1NTAcd3d3WHv
8f3iiy/EbTSGHbwiInoRcRkMgS9lkXq4vFxONTfL/7z2mryYmyuJer2Mjo+X0fHxYtfrZV1urjy+
caOcam5m8NKAiP2udCIaMEuWLJFnnnlGmpqaZN++ffLll1+K3W4XEZGkpCQREbl69WogfHv/bTAw
GAxSXl4u5eXlnG2h7xyOfIkGMa1WK5WVlbJ582YpKSmR3/3ud4HHTCaTaLVa6ejoiGjk63Q6pbmr
S3wRvE6fiFzo7haHwxHBWW6Msy30XcPwJRrkampqxOfzidVqlS1btvR5zGw2S3t7u3R1dcnZs2fD
Ct9YlBMlGuwYvkSDXFxcnFRUVMibb74pJ06ckOPHjwceS0hIkK+++iriaefKqirZYLGE/Ro3WK1S
WVUV9vOJbjUMX6IhYN26ddLa2ir5+fl9Fl65XK4+4RtuU4WBaHxBdCtj+BINATabTe655x754IMP
pK6uTq5evSoiIsOHD5fLly9Ld3d32NPOIrdmByiigcTwJRoiXn31VTl//rzExcXJ22+/LSIiI0aM
kI6ODuns7Ix4tfPD5eWydMUKmWoySUMQxzdIT2WppTU13O5DQw7Dl2iI8Hq9MmXKFLl06VJg6jkt
LU26urqk/VpZSKvVGtE1fvLEE7J682aZlZAgd1ssUi8iV772uE9EdovINKtVZiUkyOpNm+QnTzwR
0TWJbkUMX6IhpLa2Vs6fPy9/+MMfpK2tTdLT08Xn88mXX34pycnJ31o7ORgscEH07VhekmiIyc7O
ltOnT8vq1aslJydHJk2aJHfddZd0dXXJwYMHo349Frgguh7Dl2iI2b9/v5SUlMgwk0nar1wRk88n
Wo1GWgGZePvtUllVJWVlZVwARRRDnHYmGkJ27dwpj5SVSaGiyCsdHdLi80mziJzz+6UNkCWNjbJp
wQIZ6XbLrp07B/rlEg1aHPkSDRH/u2aNvFBdLf/X0SH533Jsg/RsAVpaU8MFUUQxwPAlGgLYZJ7o
u4XhSzTIdXV1ySiPR/a2tcmEEJ/bICKzEhLkVHMz7wETRRHv+RINcvX19TLe7w85eEVE8kUky++X
+vr6aL8soiGNI1+iQa4oN1eWNDZKuJWTd4vIutxcOXD4cDRfFtGQxvAlGsRaW1vF63ZLi88nujDP
4RMRu14vp5ubuUeXKEo47Uw0iH3xxRfiNhrDDl4REb2IuAyGQKEMIoocw5eIiEhlDF+iQczpdEpz
V5f4IjiHT0QudHeLw+GI1ssiGvIYvkSDmM1mk7xx4+SPEZxjj4hMyMri/V6iKGL4Eg1ylVVVssFi
Cfv5G6xWqayqiuIrIiKudiYa5Fhkg+i7hyNfokHOaDTKutpaud9kklMhPO+U9NR3Xldby+AlijKG
L9EQ8HB5uSxdsUKmmkzSEMTxDdJT13lpTQ3rOhPFAKediYaQXTt3yuKFC2W83y+V7e0yWySwB9gn
PYurNlit8rGiyLraWgYvUYwwfImGmO7ubqmvr5cNK1fKBx9/LK5rU8oXurtlQlaWVFZVSWlpKaea
iWKI4Us0hLW2tgYqVzkcDm4nIlIJw5eIiEhlXHBFRESkMoYvERGRyhi+REREKmP4EhERqYzhS0RE
pDKGLxERkcoYvkRERCpj+BIREamM4UtERKQyhi8REZHKGL5EREQqY/gSERGpjOFLRESkMoYvERGR
yhi+REREKmP4EhERqYzhS0REpDKGLxERkcoYvkRERCpj+BIREamM4UtERKQyhi8REZHKGL5EREQq
Y/gSERGpjOFLRESkMoYvERGRyhi+REREKmP4EhERqYzhS0REpDKGLxERkcoYvkRERCpj+BIREamM
4UtERKQyhi8REZHKGL5EREQqY/gSERGpjOFLRESkMoYvERGRyhi+REREKmP4EhERqYzhS0REpDKG
LxERkcoYvkRERCpj+BIREamM4UtERKQyhi8REZHKGL5EREQqY/gSERGpjOFLRESkMoYvERGRyhi+
REREKmP4EhERqYzhS0REpDKGLxERkcoYvkRERCr7f2UJdrvMwouSAAAAAElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>A bit basic but gives a general idea. If you want to make a much better looking and more informative visualization you could try <a href="https://briatte.github.io/ggnet/">R</a>, <a href="https://gephi.github.io/">gephi</a> or <a href="http://visone.info/">visone</a>. Exporting to them is covered below in <a href="#exporting-graphs"><strong>Exporting graphs</strong></a>.</p>
<h1 id="Making-a-citation-network">Making a citation network<a class="anchor-link" href="#Making-a-citation-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The <a href="{{ site.baseurl }}/docs/RecordCollection#citationNetwork"><code>citationNetwork()</code></a> method is nearly identical to <code>coCiteNetwork()</code> in its parameters. It has one additional keyword argument <code>directed</code> that controls if it produces a directed network. Read <a href="{{ site.baseurl }}/examples/#Making-a-co-citation-network"><strong>Making a co-citation network</strong></a> to learn more about <code>citationNetwork()</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>One small example is still worth providing. If you want to make a network of the citations of years by other years and have the letter <code>'A'</code> in them then you would write:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[33]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">citationsA</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">citationNetwork</span><span class="p">(</span><span class="n">nodeType</span> <span class="o">=</span> <span class="s">&#39;year&#39;</span><span class="p">,</span> <span class="n">keyWords</span> <span class="o">=</span> <span class="p">[</span><span class="s">&#39;A&#39;</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">citationsA</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 18 nodes, 24 edges, 0 isolates, 1 self loops, a density of 0.0784314 and a transitivity of 0.0344828
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[34]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">nx</span><span class="o">.</span><span class="n">draw_spring</span><span class="p">(</span><span class="n">citationsA</span><span class="p">,</span> <span class="n">with_labels</span> <span class="o">=</span> <span class="k">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAeAAAAFBCAYAAACvlHzeAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzs3Xd8zlf/x/FXEtlbBoqQIlEr0UTUnrW1alRQGtRsa1Qq
1Vqt+lFKB01vW63ooEq56c1dVHEjmtgzrU1JJITsfH5/XEmaSIwMruDzfDyuR7i+45zvdbXeOed7
vueYiIiglFJKqUfK1NgVUEoppZ5GGsBKKaWUEWgAK6WUUkagAayUUkoZgQawUkopZQQawEoppZQR
aAArpZRSRqABrJRSShmBBrBSSillBBrASimllBFoACullFJGoAGslFJKGYEGsFJKKWUEGsBKKaWU
EWgAK6WUUkagAayUUkoZgQawUkopZQQawEoppZQRaAArpZRSRqABrJRSShmBBrBSSillBBrASiml
lBFoACullFJGoAGslFJKGYEGsFJKKWUEGsBKKaWUEWgAK6WUUkagAayUUkoZgQawUkopZQQawEop
pZQRaAArpZRSRqABrJRSShmBBrBSSillBBrASimllBFoACullFJGoAGslFJKGYEGsFJKKWUEGsBK
KaWUEWgAK6WUUkagAayUUkoZgQawUkopZQQawEoppZQRaAArpZRSRqABrJRSShmBBrBSSillBBrA
SimllBFoACullFJGoAGslFJKGYEGsFJKKWUEGsBKKaWUEWgAK6WUUkagAayUUkoZgQawUkopZQQa
wEoppZQRaAArpZRSRqABrJRSShmBBrBSSillBBrASimllBGUMHYF1MMXFxdHdHQ0AC4uLjg6Ohq5
RkoppbQF/IRKSkoiLCyMRr6+lHVzo4WPDy18fCjr5kYjX1/CwsJITk42djWVUuqpZSIiYuxKqKL1
7cqVDB80iJoiDL15k47809WRAqwDQu3sOGRqyhdz5tA9MNB4lVVKqaeUBvAT5suZM/l07Fh+TEjA
7z77hgOv2NgQPGkSw95551FUTymlVAYN4CfItytX8m6/fuxISMDjAY85CzS0sWH6ggXaElZKqUdI
7wE/hpKTk+nfvz8VK1bEwcGB2rVrs27dOoYPGsSahAROAlUBW6A5hpDNLgRwzXiFAj/evs3wQYNI
Tk5m3Lhx1KxZE3Nzcz788MNHel1KKfU00QB+DKWmpuLh4cH27du5ceMGH3/8Md27d6dyaioeQGdg
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
gg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-co-author-network">Making a co-author network<a class="anchor-link" href="#Making-a-co-author-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The <a href="{{ site.baseurl }}/docs/RecordCollection#coAuthNetwork"><code>coAuthNetwork()</code></a> function produces the co-authorship network of the RecordCollection as is used as shown</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">coAuths</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">coAuthNetwork</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">coAuths</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 45 nodes, 46 edges, 9 isolates, 0 self loops, a density of 0.0464646 and a transitivity of 0.822581
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-one-mode-network">Making a one-mode network<a class="anchor-link" href="#Making-a-one-mode-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>In addition to the specialized network generators <em>metaknowledge</em> lets you make a one-mode co-occurence network of any of the WOS tags, with the <a href="{{ site.baseurl }}/docs/RecordCollection#oneModeNetwork">oneModeNetwork()</a> function. For examples the WOS subject tag <code>'WC'</code> can be examined.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">wcCoOccurs</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">oneModeNetwork</span><span class="p">(</span><span class="s">&#39;WC&#39;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">wcCoOccurs</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 9 nodes, 3 edges, 3 isolates, 0 self loops, a density of 0.0833333 and a transitivity of 0
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[37]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">nx</span><span class="o">.</span><span class="n">draw_spring</span><span class="p">(</span><span class="n">wcCoOccurs</span><span class="p">,</span> <span class="n">with_labels</span> <span class="o">=</span> <span class="k">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAd8AAAFBCAYAAAA2bKVrAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzs3XlcVNX/x/HXDItsM+yg7CAtgltpbrllX62+ZZqaorn9
NKXFby4ttmhamn2tLMu+lRVZmoItprmk5VJpZWa5pOaCCiRqgoKArMLn98fADRSUXEbLz/Px4KEz
98695965zJtz7jlnTCIiKKWUUspuzJe6AEoppdSVRsNXKaWUsjMNX6WUUsrONHyVUkopO9PwVUop
pexMw1cppZSyMw1fpZRSys40fJVSSik70/BVSiml7EzDVymllLIzDV+llFLKzjR8lVJKKTvT8FVK
KaXsTMNXKaWUsjMNX6WUUsrONHyVUkopO9PwVUoppexMw1cppZSyMw1fpZRSys40fJVSSik70/BV
Siml7EzDVymllLIzDV+llFLKzjR8lVJKKTvT8FVKKaXsTMNXKaWUsjMNX6WUUsrONHyVUkopO9Pw
VUoppexMw1cppZSyMw1fpZRSys40fJVSSik70/BVSiml7EzDVymllLIzDV+llFLKzjR8lVJKKTvT
8FVKKaXsTMNXKaWUsjMNX6WUUsrONHyVUkopO9PwVUoppexMw1cppZSyMw1fpZRSys40fJVSSik7
0/BVSiml7EzDVymllLIzDV+llFLKzjR8lVJKKTvT8FVKKaXsTMNXKaWUsjMNX6WUUsrONHyVUkop
O9PwVUoppexMw1cppZSyMw1fpZRSys40fJVSSik7c7zUBVDq+PHjHD16FABfX188PT0vcYmUUuri
0pqvuiSKiopITEykXdOmBPv7c3OTJtzcpAnB/v60a9qUxMREiouLL3UxlVLqojCJiFzqQqgry/yk
JEbGx9NIhAdyc+nKn00wJcBi4A0PD7aZzbw6cyZ94uIuXWGVUuoi0PBVdvXayy/z0rhxfFZQQLOz
rPszcJebG49MmsRDY8bYo3hKKWUXGr7KbuYnJfHokCGsKygg7CzrpgGxwDagnZsbLyYkaA1YKfWP
ofd81QXz/vvv06hRI9zd3alXrx4PPPAAx48fB2z3eEfGx7OwhuCNAFZXehwG5ALhwGf5+YyMj9d7
wEqpfwwNX3VBTJs2jccff5xp06aRk5PD+vXrSU1NpXPnzpSUlLBgwQIalpVxfQ2vNwE1NcE0A2LL
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
CuwHrgFSgXSgL3AtMBMILf8pA7yxjS1eBrwKOJnNeHl5GecObPfZExISmDZtGldffTWvvPIKERER
ADRo0ACTycTu3bt58cUXEREOHTpklNlsNpOXZzvChIQEdu/eTYMGDWjRogW///47x44d49577z3j
NVPdeTibsrIyunbtynXXXcfBgwdZtWoV06dP58svvwRg2rRpJCUl8cUXXxjH5+bmxrfffgvA1q1b
yc3N5e677wbgjz/+ICsri7S0NOMPwA0bNrBlyxa2bNnChg0bal3+Uw/mslBSUiKrV68+52aegwcP
iru7u2RnZxvbCwgIMO7lVJadnS1ujo4SCdKlvAmotvd8h4DcW6kpqHI3/Li4OJkyZYqIiBQVFcl3
331n7M9kMsmaNWuM8q1Zs0YcHR3l8ccfl+LiYikoKJDx48dL69atJSMjQzIyMqRNmzZGU3LF+g8/
/LAUFxfLN998I+7u7lXOla+vr/z0009y8uRJueeeeyQuLk5ERDZs2CBBQUFSVlYmIiIZGRni5uYm
R44ckZ07d0poaKgcOnRIRERSU1ON5vGJEycazVApKSlisVgkKSlJTp48KUePHpUtW7aIiEjdunWN
Jvjs7Oxqz7n65wsPDxcPDw/x8vIyfiruF86aNUuio6ONdU+cOCEmk0n++OMPSU1NFUdHRykoKDCW
9+/fX/r37y8REREyd+5cMZlMcs0118j3338vHTt2lOeee85Y94033pD27duLyWSSKVOmSM+ePcXV
1dVogr7lllvkgw8+kMOHD0udOnWkc+fO8uqrr4qIyLx584zPkCeeeELMZrPxeyIi0rJlSwkLCxMR
260dwPi9fuedd8Tf31+mTp1qrGs2m43X1q1bVwBxc3SUYpD+IBMrfZa8U37fV0AWljc7e5X/eJY/
fr/SZ01MTIzk5+fLPffcI3fffbeYTCaZOXOmjBkzRgB5BeR7EAeQz6r57HoCxAlkW6XnnMs/AwXE
08lJunfvXuUWVr169aRLly4iInLzzTfLG2+8YRzfrl27xMnJSUpLS2X//v22MrzyiojYPq/q1KlT
bTNxUlKSmEwmeffdd+WOO+6QIUOGGOf8xhtvlCVLllR7fXXo0EHc3NyqXF9PP/20sb+KZuf169cb
71mFKVOmyP/93/+JiMjVV19d5V5+ZafeHlyzZo04OztX6W1ev359+eKLL4zHK1asqHZbZ3PZ1Hwd
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
Hz4cHx8fIiIi8PPz49FHHwVqN/i7rKyMV155heDgYHx9fVm7di1vvvkmYJsiMSIi4owzaFU3MHzg
wIGEh4cTHBxMw4YNad269WkD75vfeKMxhRzYZq/ZgW06tx7V7GcM0Js/p4B71mxmwP33n1aGqVOn
Eh0dTatWrfD09KRz587s3r0bgD179tC5c2csFgtt2rThwQcfpEOHDqft63wGtdc0UL7CyJEjufPO
O+nSpQtWq7XaKf8qzJs3jx9//BEfHx+effZZBg0aZCw7fPgwd999N56ensTExNCxY0edgEMp9Y9l
krNVbf5BnnvuOQICAmrVDP1XFRUVER4QwLKcHK4/++pV/AzcbrWSlpGh92GUUuoKcEWF78U2PymJ
R4cMYV1BAbX9nos0oK2bGy8mJNCnfFpNpZRS/2yXXbPz31mfuDgemTyZtq6u/FyL9X/GFryPTJqk
wauUUlcQrfleBPOTkhgZH0/DsjIeyMvjTv78ZqMSbN8g8obFwnaTiVdnztTgVUqpK4yG70VSXFzM
ggULeGPqVH7Zvh2/8nu5mcXFXB8bywNjx9KjRw+9x6uUUlcgDV87OH78uPF9kT4+PjrWTimlrnAa
vkoppZSdaYcrpZRSys40fJVSSik70/BVSiml7EzDVymllLIzDV+llFLKzjR8lVJKKTvT8FVKKaXs
TMNXKaWUsjMNX6WUUsrONHyVUkopO9PwVUoppexMw1cppZSyMw1fpZRSys40fJVSSik70/BVSiml
7EzDVymllLIzDV+llFLKzjR8lVJKKTvT8FVKKaXsTMNXKaWUsjMNX6WUUsrONHyVUkopO9PwVUop
pexMw1cppZSyMw1fpZRSys40fJVSSik70/BVSiml7EzDVymllLIzDV+llFLKzjR8lVJKKTtzvNQF
uJwdP36co0ePAuDr64unp+clLpFSSql/Aq35nqKoqIjExETaNW1KsL8/Nzdpws1NmhDs70+7pk1J
TEykuLj4UhdTKaXU35hJRORSF+JyMT8piZHx8TQS4YHcXLryZ9NACbAYeMPDg21mM6/OnEmfuLhL
V1illFJ/W1rzLffayy/z6JAhLM3J4avcXO4C1gGh5cudgB7Ayrw8lubk8OjQobz28st2L2dERASr
Vq2y+36VUkpdOH/L8F2xYgXt27fHarUSEBBAx44dWbx48Tlvb35SEi+NG8e6ggKa1WL9ZsC6/Hxe
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-two-mode-network">Making a two-mode network<a class="anchor-link" href="#Making-a-two-mode-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>If you wish to study the relationships between 2 tags you can use the <a href="{{ site.baseurl }}/docs/RecordCollection#twoModeNetwork"><code>twoModeNetwork()</code></a> function which creates a two mode network showing the connections between the tags. For example to look at the connections between titles(<code>'TI'</code>) and subjects (<code>'WC'</code>)</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">ti_wc</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">twoModeNetwork</span><span class="p">(</span><span class="s">&#39;WC&#39;</span><span class="p">,</span> <span class="s">&#39;title&#39;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">ti_wc</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>The graph has 40 nodes, 35 edges, 0 isolates, 0 self loops, a density of 0.0448718 and a transitivity of 0
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The network is directed by default with the first tag going to the second.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[39]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mkv</span><span class="o">.</span><span class="n">quickVisual</span><span class="p">(</span><span class="n">ti_wc</span><span class="p">,</span> <span class="n">showLabel</span> <span class="o">=</span> <span class="k">False</span><span class="p">)</span> <span class="c">#default is False as there are usually lots of labels</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAX4AAAEACAYAAAC08h1NAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzs3XdYU9cbB/BvwkxYIqKoKK2K4h64kKqAAwVcdVARURHR
tlo3bmvrwgUOVNx1j1onuK3iAPdeuBUHWGSTkITk/f0B5AcSRiAQIOfzPPdRcu899w3jm5ubc8/h
EBGBYRiG0RhcdRfAMAzDlC4W/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzDaBgW/AzDMBqGBT/DMIyG
YcHPMAyjYVjwMwzDaBgW/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzDaBgW/AzDMBqGBT/DMIyGYcHP
MAyjYVjwMwzDaBgW/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzDaBgW/AzDMBqGBT/DMIyGYcHPMAyj
YVjwMwzDaBgW/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzDaBgW/AzDMBqGBT/DMIyGYcHPMAyjYVjw
MwzDaBgW/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzDaBgW/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzD
aBgW/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzDaBgW/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzDaBgW
/AzDMBqGBT/DMIyGYcHPMAyjYVjwMwzDaBhtdRfAMIx6pKSk4OHDhzkea9myJfT19dVUEVNaWPAz
jAaKjY1FVzs7cGJioM/NeOOfLJXCrEEDhF68CENDQwDA5s3bcPFihHw/PT0dzJ3rBysrK7XUzagG
h4hI3UUwDFN6skK/5/v3WCQWg5P5uAzAKH19vGzcGKEXL2LNmvVYsGAjBIIpQOZWXO5LmJsfxPXr
F1j4l2Ms+BlGgwiFQtg1a5Yr9LNkhf/lymb4EK8PofAiAMsc23C5a2BuHsjCvxxjwc8wGuTJkyfo
064dnqek5Ar9LDIAhgCEeACgqcJtuNxAWFvvxrNnt0qoUqYksV49DKNhdDicPEMfyAgFLrgAauS5
jUw2EDEx0aoujSklLPgZhmE0DOvVwzDlwPPnzxEeHi7/msvlolevXjA1NVWqHQ6Hg6T0dKQByKvT
ZhIACQjI930BU56xa/wMU8bduXMHPR0c0E0mk5+pfSFCtKUlzkVEoHLlyoVuSyqV4qc+fSC4cAH/
CAS5wj8JgKOWFh5LdSHCawAWCtvhctejTp0NePHiXlGeEqNmLPgZpgzLCv31ycn4MdvjBMBPVxfn
v/tO6fCXSCTw6NcvV/gnAXDQ0kKtrl3RxLYdVq78GwLBv/g2/LncTTA1nY9r1/5FvXr1ivkMGXVg
wc8wZdTHjx/RqmHDXKGfJSv8w+rVw43Hj5VqWyKRYGj//vg7JATIigAOB2NGjMCaTZvA5XIxZ86f
CAjYB4FgOrIu+3A4L1G58jYW+uUcu8bPMGXUq1evUJ/LVRj6QEYULxGLofXkiVLtikQi7N27F7EC
AWbNno2IiAiEhIRAS0sL2tr/j4T58+fC3LwK/v33rPwxfX0dLFjAQr+8Y8HPMGVYQR+vKvPx69ev
XxEcHIzz589j8ODBOH78OHg8Hnr16gU9PT2F+/z22y/47bdflDgKUx6w4GeYCu7FixcIDAxEVFQU
xowZgxkzZoDL/X9Pbna1V/Ow4GeYMkpXVxcf09ORDMAoj20iAehqaeV6nIhw+fJlrFmzBnw+HxMm
TEDLli1LslymHGHBzzBlVNu2beHUrx9cDh3CCYEgV/g/A9CFx8OGoCD5YxKJBAcPHsS2bdvQqlUr
rFy5EjVr1izVupmyjwU/w5RB9+7dw7t37+Dy44+IioqC8/Xr2JaWJv+DjQHQX08Pi4OCMNzbG4mJ
idi8eTNCQ0PRr18/HDp0SD60ckE4HHajlqZhwc8wZczBv//Gr8OHo31mDxtdIrxOT0cnHi8jzDkc
EBFq1a4Nxy5dMGnSJDx9+hSjRo3C2bNnoaXg0k9exGJxjp48jGZgP3GGKUMO/v03xg4bhjNCIZpn
ezweQFddXXQeOBArgoJw8+ZNeHp6wtfXF3/88Qfat29fpOMlJyfD2NhYJbUz5QcbpI1hyohz585h
7LBhOP1N6AOAKYBzAgH+3bIFjevVw969e7F9+3bw+fwihz7Agl9TseBnSs3JkydRic+Hrra2fGlW
ty4+ffqk7tLKhKtXr2KUgtDPYgpguUgEc0NDBAYGws7ODlZWVjkGb1NWUlISjIzy6jPEVFQs+JlS
cfLkSQwbMAChQiFSpFL58tP793Bq1w6fP39Wd4llQkF/kFwgxzX86dOnw9/fv8jHS0pKKvYZ/4MH
D1CjcmVocbnyxcLUFHfu3ClWu0zJYcHPlLhTp05h2IABOCoQwB6AbrZlZno6vKKj4di2LaKj2cQe
yrKwsECDBg0QFhZWpP2LG/wPHjyAc8eOWBkfDzGRfFmXkICeDg4s/MsoFvxMiVswdSrWCwSwy2P9
zPR0tI2Jwc6dO0u1rrJGS0sL7wrokfMOgLaubo7H/Pz8sHTp0iLdgZucnFzkSz0PHz6Ec8eOWJWU
hEEAtLItPwIITk5GTwcH3LvHhm4ua1jwMyVOJpWiegHbVJfJIJPJSqWessrHxwfXa9bEnzo6Ctef
BjDNwADzAgJyPG5ubo7mzZvj/PnzSh+zOGf8QcuW4dfM0FekH4DJyclYuXBhkdpnSg4LfoYpIyws
LHDh+nXsrV4df+roIA6QLyEABmppYWlQEDp06JBr38mTJ2P58uVKn/UXJ/hl6emoVsA2FpnbMWUL
C36mVEiLuV5TZIV/iLU16vH58uWXKlWw//hx7NixAzExMbn2MzMzQ7t27XDq1CmljleWunOePXsW
zb7/Ho0sLeWLj4cHJBKJukurcNgNXAwA4Mjhw1jn7///STkADBkzBsO8vYvddo9+/fDbu3c4JxDA
TMH6ywB26OnhuINDsY9VEVhYWOQ5sYqVlRWGDx+Ow4cPQ18/58SJEydOxKBBg9CjR49CD8NQ3O6c
BZ3LF/Zc/8yZM/Ds1w9bBQLUyXyMAPgdPYohP/6I3YcOQSePS2BMERCj8f4+cICq8Xh0AKDTmcsR
gGrx+bRx/fpity+TyWjq+PHUgs+n2IyXFvlyCSBzPp/Onj2rgmeiGUJDQ2n48OEkk8lyrZs/fz4d
PXq00G2NHDmSPn/+XKQ6Dh44QDV4PHr6zc80a3kOkCWPR3t37863ndOnT5M5n09XFLQhBMiFz6eB
bm4kFouLVCeTGwt+DZcV+vcU/NG9KIHwt+LzqZ22NjmZmJCTiQlVYaFfJCtWrKAlS5bkejwpKYm6
dOlCUqm0UO0MHDiQUlNTi1xHYEAAmXG5ucI/K/Q3bdhQYBvfmZvTmTxePAigNIBsDQzo0KFDRa6T
yYkFvwZLSkoiA11dhaGfPfwr6enRu3fvin08mUxGZ86cIQcHBzp37hydO3eOXrx4oYJnonlkMhn5
+PgoPLv39/engwcPFqodV1dXhe8cCiMhIYG6dOlCixctoqo8HnU2MZEvVQsZ+kRE1U1M6GM+v4ME
kLuREe3du7dIdTK5sWv8GkwkEkGfy81ziAAAqAfAQlcXqampRTqGRCLBly9f5F8nJyeje/fu6NKl
S5HaYzJwOBwEBQWhX79++P7779G0aVP5urFjx6J3797o169fjpm28mtLWWKxGJ6enliwYAHat28P
t169EBsbK19vZmaWoyambGHBz5SYhIQEOP/wA96+egXtzABKFonQ2dERsmnTChVKpWHPrl3Yt2mT
/GsOl4tfpk+Hs7OzGqsqmJ6eHv766y+4u7vjwIEDMDc3BwAYGBjA1dUVBw4cwE8//aTy48pkMvj4
+GDUqFHyAeKaNGlSrDYL6oTKJodUMXW/5WDU57///iMzff1832ITQDZGRvTkyROl2o6Pj6e2jRvT
b7q6JMvWVhJA9jwe+Xp5Ffo6dEnasmkT1eTxaD9ARzOX7QCZ83gUGhqq7vIK5cGDB9SzZ08SiUTy
xwQCATk6OlJ6enq++7q5uSl9vMmTJ9PGjRuV3u9bQqGQ1q9fTzVNTGiYtjZJ8/j9u5rZAeDevXt5
thUTE0MPHz6UL69evSp2fRUZC34NJhAIqJqJCe3LJ/RPAVTF0JC+fPlS6HZTUlIUhn728P+Bz6ef
R4wowWdXsKzQj1RQY0Q5C/+jR4+Sj49Pjuv1q1evph07duS7n6urq1LHCQgIoN9//70oJcolJiaS
v78/OTk50fbt2ykuLo46tmpFI/X1c4V/VuifOnUqz/YiIiKoiqEhNTY2li+V9fVp1YoVxaqzImPB
r+Hu379PFnmE/ymAzA0M6OrVq0q1eenSJWphaKgw9LOHvzrfcL5584ZM9fUVhn728DfU0ytWr5fS
5O/vTwEBAfKvhUIhOTg4kEQiUbi9TCZTKvj37t1Lvr6+Rf4wOCYmhmbOnEndu3enw4cP53jHl5yc
TB1btaJufD758njky+PRKB6vUKFvbmBAJ7752b0F6Hs+n4V/Htg1fjWTSqXwGzcONy5flj+mq6+P
pcHBsLW1LfHjN2vWDKcvXYJzp064mZgIk8zHhQDW6ejgxJkzCocIKIihlhby+8hQ3SPAJycno6au
LuqnpeW5TXsAWkQQi8Xg8/mlV1wR+fn5wdvbGydPnkTPnj2hr68Pd3d37NixA94KbsQTCoWFfl7/
/vsv/vnnH+zdu1fpD4PfvXuH5cuX4/379xg/fjwWLFiQqw1DQ0OcCAvDgQMHctyp62tri9atWyts
9+7du+jdtSu2p6ai5zfrrABcEAjgOGcO9PT0MPrXX5WquaJjwa9GUqkUIz088D4kBAsFAnlQRgJw
cXTEiQsXSi38/42IwJ7duyHOvHOXC6DppUuoV69eiR+fUQ0Oh4P169ejb9++sLKyQqNGjeDt7Q1n
Z2d4enpC95tRPQs7Muf9+/exdOlSHDp0SKn5eZ88eYKlS5dCJBJh8uTJeQZ4FkNDQ4UvUHkJDQ2F
l0CQK/SzWAFYLxBg0caNLPi/wYJfTbKH/nGBAAbZ1nUEYJ6cXKrh37BhQ8xfsCDHY5cuXcKSJUuw
YsUKpdsTyGQgIM+zfoHyJaqFVCot0nDH6qKvr4+//voLgwcPxsGDB2FmZgZPT09s27YNo0ePzrFt
YQZoe/fuHSZOnIgDBw4U+t3B9evXsWLFChgbG2P69OmwsbEp8vMpiH4x12uqstGfTgMdPnwYD0JD
c4V+lj4AViYnY1j//qVdmlynTp3w8uVLpWfHatGiBah6dUzX1VXYDU8AwI3Ph/fgwSqpsyiqVKmC
D2IxLuWzzUFkDCm9fNGichX+FhYWCAgIwLBhwyAWi+Hl5YX9+/dDJBLl2K6g4P/69StGjBiBLVu2
oEqVKvkek4hw9uxZ9OrVC3v37sWKFSuwefPmEgl9sViMO3fu4NatW5CVo59LWcKCX01SU1PRFFAY
+lnaARAI1HtuPGPGDCxevFipfYyMjHAuIgJnv/suV/hnhX5tNzdsVNPEKwKBAIGBgWjVoQP66uoq
DP9/AIwFcBzAsXXrsGr58tItsphatmwJb29vjB8/Htra2hg+fDg2ZbtXAch/ZE6hUAhPT0+sWLEC
33//fZ7HkUqlOHjwIJydnXH58mVs27YNK1euRK1atVTyPMRiMW7fvo2NGzdi9OjR6NGjBwYMGICD
Bw+Cx+MhsYB7QRKQcV8G8w01f7issf766y/yMjDIt//8K4C+NzdXd6nUr18/ev/+vdL7ff36lVrW
r0+WPB7V0Nammjo6ZK6vT8MGDSqwf3lJOX36NDk4ONDx48eJiKiviwtVAuhPgJZmLjMBqgbQ3cyf
wwGA+nfrppZ6i2v+/Pm0evVqkkgk5OjoSAKBQL7u6NGjtEHBsArp6ek0cODAfMdQEolEtGXLFnJ0
dKRly5ZRUlJSsWtNS0ujmzdvUnBwMI0aNYqcnZ2pd+/eNHPmTPrnn3/o7du3OXoUvXjxgmqYmtJf
HI7Cv5/7AFnweHTw77+LXVtFw67xMwWaOXMmFi1ahPXr1yu1X+XKlRHx4AG2bNmC8+fPo3PnzujV
qxe+++67Ig0TUBz//fcfpkyZAlNTUxw/fhyGhoYAgFo1a2IYgKTMBcj4XOIsgKbZvqZyOjvYrFmz
4OXlhQYNGmDUqFEIDg7GxIkTAfx/SGbKdrmEiDBu3Dj07dsXXbt2zdVeamoqNm3ahGPHjmHw4ME4
efIk9PT0lK5LJBLhwYMHuH37Nm7fvo2oqCjo6emhadOmsLW1xezZs1GrVq18f0/q1auH8+Hh6NKh
A5CQgGHZnscDAM48HlZt24b+AwYoXV9Fx4JfTerWrYsZRHgKoKGC9QRgGZcLmUyG27dvl8oHvHlp
3bo1li5dirdv3+K7775Tal89PT0kJCSAw+HAxcUl38sGJYGIsHPnTuzYsQOLFi1C27Ztc21TB8Bv
BbRz//59uLm5gYhgYmKCWrVqoXbt2qhdu7b8/6ampqX+glYQDoeDjRs3om/fvggMDMTmzZvh6+sL
AwMDHD0agn/+OQgPDw/59hYWdfHLL8NyPAYAcXFxCAoKwuXLl+Hj44OzZ89Cq4D5gbOkpaXlCPkP
Hz5AX19fHvJz586FpaVlkb53NjY2OB8ejq729piQbTwpsUyGbdu2YZC7u9JtagIOEft0RF12bt+O
6T//jHNCYY7wJwDjdXVxrV49bN67F8HBwYiJicG0adMUBldpuH//PoKCgnJdJy6MYcOG4ePHjzhz
5kypjs/z6tUrTJo0CR06dMCkSZMUTuQxaexYyNavx8p8zuiXcji44+KCfSEhAIDExERERUXh/fv3
8n/fv3+P+Ph4EBG4XC4sLCzkLwjZ//128pTS8unTJwwZMgRDhw7F3r0H8fVrCu7dewoiJ2RMkPgH
ABNwuWPQqNF9XLlyGiYmJvj48SMCAgLw7NkzjB07tsBJXtLS0nD//n15yH/8+BH6+vpo1qwZbG1t
YWtri5o1a6r8BVIkEuX4PExXVxcGBvl9gqbZWPCrWVb4e4lE8q6Pz7W18b5ePZy5ehWVKlUCAHz4
8AFLlizBhw8f4OfnBzs7u1KvdfDgwZg/f77SfftdXFwAACdOnCiJsnKRSCQICAjA1atXERgYiLp1
6+a5bVRUFBzbtcOvX75gojT3BJC7ORxMNTHB2StX0Lhx40IdXyaTISYmRv6CkPXi8OHDBwiFQgAZ
3S4tLS1zvWuwsLAosRfHGzduoF8/D3z+XAlEP2dbE46MiyNnAZhAT28crKzCYWfXDCkpKZg4cSLs
7e1ztScUCnOE/KdPn8Dj8XKEfI0aNUrtXVBaWlqO8NfT02PhnwcW/GXA6dOncfv2bfnXurq68PHx
kYd+dp8+fcLSpUvx+vVr+Pn54Ycffii1Oh8/fozly5dj27Zthd6HiODo6IgWLVpg5cqVJVhdhps3
b2LGjBnw8vLC0KFDCxU6WeE/+ssXeGYL/9McDmYqGfqFlZaWhg8fPuR61xAdHQ1Z5rsPU1PTXC8M
tWvXhomJSQGt5yaTyeDl5YuDB59AJDoDwDDbWgIwEcBVZIW/trYdliwZhEmTJgHI6AmVPeQ/f/4M
Pp+fK+TV5cGDB+jeqRPE2e7EFhNh1/796Nu3r9rqKqtY8JdT0dHRWL58OZ49e4YpU6bAoZTmq/Xy
8sLMmTML3T87JiYG7u7u8Pb2hpeXV4nVlZKSgtmzZyMhIQHLli2TD1FcWFFRUejXrRs+ZrtnwbRS
Jfx94oTKQ78wiAgJCQm5XhiioqKQkJAAANDS0kL16tVzvTDUrFkz1weu69evx+TJOyAUnkXO0Jcf
ERkdWOMA7AWf/yPc3StBJpMhOjoaPB4PzZs3LxMh/60HDx7AuVMnrExMRPYr+ncA9OTxsGHPHhb+
32DBX859+fIFK1aswKNHjzBp0iQ4OTmV6FvryMhIzJ8/H7t27SrU9mFhYZg7dy6CgoJKbGKO0NBQ
LF++HDNmzED37t1L5BhlkVQqxefPn3O9MERFRUEsFoPD4YDH46FWrVp4/PgxzpyxAzAvnxbPA1gE
4Dx0dXtj4sRGGD9+PKpXr14qz6conjx5gi4dOuQK/SxZ4b95/3706tWrtMsrs1ivnnKuatWqWLJk
CWJjYxEYGIgVK1ZgwoQJ6NatW4m8ADRo0AC6urp49OhRoSbfiIyMhEAgQMOGivouFU90dDQmT56M
mjVrIiQkROOu52ppacHS0hKWlpZ5fuYjEAgQFRWFhQsXKtW2TCbC9evX8ccff0BPTw/6+vrQ09Mr
0v+//VpHR0dlv5u7d+7E0DxCHwBaAVgtFGLtokUs+LNhwV9BVKlSBQsXLkRcXBxWrlyJgIAAjB8/
vsBeGEUxe/ZszJw5E/v27Stw26dPn4LH4yk1uFdBiAhbtmzB/v37sXTpUrRs2VJlbVckIpEI9+/f
x9WrV3Hr1i1kdFwtjB3gcq9jypTdaN68OUQiEdLS0iASieRL9q/T0tKQmJio8HFF/88afTPrYkN+
v586Ojr5vqDcuH4dDgU8G5OMgxXyuWsGFvwVTOXKlfHnn38iPj4eq1evRmBgIMaNGwc3NzeVvQDU
qVMHxsbGuHfvHlq0aJHvto8fP0aDBg1Uclwg4x3EpEmT0LVrV5w8eVKlLyjlXWxsLMLDw3H16lU8
fPgQWlpasLW1hb29PUaOHIk5cw5BKJwKxQOFEICjAEQwMvJDx472GDNmDOrUqYPq1aujXbt2aN++
PVq1alWkG7aKgoggkUjyfRF5+vhxqdRS0bBr/BVcYmIigoKCcPHiRfz666/o3bu3SroLvnv3DlOm
TMHff/+d73atW7eGr68vfH19i3U8sViMJUuW4M6dOwgMDFT6RrKKhojw7NkzedB/+vQJZmZm6NCh
A+zt7dG0adMcN1hJpVJ07uyMa9dSIZWeQ87wJwC/gcvdCyMjHYSHn0ejRo3w8uVL/Pbbb+jatSsa
NWqEa9eu4e7du5BIJLCxsUH79u1hZ2ensnF5imLWjBng+vtjfj7bHAEQ3L49TkVElFZZZR4Lfg2R
nJyMtWvX4ty5cxgzZgx+/PHHYr8AjB07FsOGDUObNm0UrheJRGjevDl27tyZ5zaFER4ejjlz5mDU
qFFwd3cvc3fHlgahUIibN28iPDwcN27cgEAgQIMGDWBvbw97e3vUrFkz3/1XrVqF+/fvIzVVipCQ
dxAIhsvXaWldhq7uMfz991+wtbWFhYWFfJ1UKsXq1atx8eJFrFmzBrVr14ZMJsOzZ88QERGBa9eu
4cOHDzA2Nkbbtm1hZ2eHVq1aldqNajdu3ICbkxP2pqaii4L1LwE48flYuHYthg4fXio1lQcs+DVM
SkoK1q9fj1OnTsHX1xcDBgwo9K333/r48SPGjRuHQ4cOKVz/+PFj9O3bFw8fPixSECQmJmLmzJny
s/3KlSsXqc7yKDo6GlevXkV4eDiePHkCPT09tG7dGvb29mjbtm2hP8iWyWTw8/ODgYEB5s2bB5lM
hnnzFuHp01fybSpVMkStWuawtLTEyJEjFbYTGRmJ8ePHY+DAgfD29s714puYmIjr168jIiICd+7c
gVgsRoMGDWBnZyd/V1BSL9iXL19G/549c4V/VujPDQiAzzdzEWg6FvylJC0tDa9fv5Z/zeFwUL9+
/SKHbnGlpqZiw4YNCAkJgY+PD9zd3YtUy4QJEzBo0CCF0zP+888/mDdvHh4+fKh0u0eOHMHq1asx
Z84cODo6Kr1/eSKTyfD48WN50H/58gXVqlWDvb09OnTogEaNGhXp3ZlIJMLIkSPh4OAAHx+ffLeV
SqVwdXXFxo0bUbt27Ty3CQgIQHh4ONasWQNLS8t8n1NkZKT8XUFUVBSMjIzk7wpsbW1V+q7g8uXL
6NezJ6pl+x3+LBZj6cqVLPQVYMFfCuLj49GhQzd8+JAADidj+jupNAUdOrREaOjfuabEU0TRj0kV
Z1BCoRCbNm3CkSNHMGLECAwePFipD0yjo6Ph6+uLY8eO5Vo3c+ZM3L17FydPnix0ex8/fsSkSZNg
bW2NWbNmgcfjFXpfVUtLS8ORI0dyzAHbrFkzNG/evFjtpqam4vr16/LeNhKJBI0aNYK9vT3s7Oxy
XGopqvj4eHh6euLXX3+VD5lRkMjISPj5+eHIkSP5/m49efIEEyZMwJAhQ+Dl5VXo38PExETcuHED
165dw+3btyESiVC/fn35u4LatWsX63c6JiYGsbGx8q8NDQ1hZWVV5PYqtBIf+FnDxcXFkY2NLenq
TiBAlm24cBHxeH2pa9feJBKJ8m3j2bNnZFmlCiHjUzgCQMY8Hl24cEFldQqFQgoKCiIHBwfaunUr
icXiQu87depUunjxYq7Hu3TpQgsXLixUG1KplNatW0fOzs704MGDQh+7pAiFQurRqRPZGxiQp6Eh
eRoa0hBDQzLn8+ncuXNKtRUVFUX79u2jcePGkbOzM/3444/k7+9Ply9fzjE+vqq8f/+eHB0d6caN
G0rvu3z5coVj9H9LIpHQwoULqX///vTp06eilElSqZSePn1KW7duJV9fX3J2dqYBAwbQ0qVLi/W9
iYuLI/sWLchAV1e+VDYwoEOHDhWpvYqIBX8JSk1NzSP0c4Z/9+59c0wwkd2zZ8+opqkpbftmsol/
AarC56s0/IkyJsNYv349OTg40KZNmwp8USIi+vLlC7m4uOR6DvXr16dLly4VuP+jR4+oR48eFBQU
pLYJWrLLCv1BPB5JvvmhXQLyDX+JREJ37tyhNWvWkIeHBzk7O5O3tzdt2bKFnj17lufPWVXu379P
Dg4O9PLlyyLtn56eTj169KC3b98WavsHDx5Q165daffu3Sp5bomJiXT27FmaP38+9e3bl5ydnWnc
uHG0Z88eevPmTYHHiIuLI1sbG5qoq0tJACVnLtcAqsrj0eHDh4tdY0XAgr8E3blzhwwNbfII/f+H
v7a2PiUnJ+fa//nz5wpD/9vwDwsLU3ntIpGINm3aRI6OjhQcHExpaWn5bj9z5swcMzbJZDKysLDI
d2YmoVAAfKm5AAAgAElEQVRIc+bMoYEDB1JUVJTKai+uQa6uCkP/2/C/d+8eJSYm0unTp2nu3Lnk
5uZGPXv2pGnTptGxY8fov//+K9W6z507R87OzvTly5ditRMZGUlubm4klUoLtb1YLKY//viD3N3d
KSYmpljH/pZMJqNnz57RX3/9RaNHjyZnZ2fq378/LVmyhC5dupTjXUF8fLw89GUKfm63M8P/yJEj
Kq2xPGLBX4Lu3LlDxsYt8ptdkQAiHR0DhcHvN2kSTckj9LOWTQD1cXQssecgFotp69at5ODgQEFB
QSQUChVu9/XrV+rRo4f8jOzz589Us2bNPNsNCwsjR0dH+ueff0r8LFhZVmZm9LqAH1p/HR1q0qQJ
DRgwgJYvX04RERGFendUUnbt2kUDBw6k1NRUlbQXGBhI69atU2qfO3fukJOTEx04cEAlNeQlKSmJ
zp8/TwsWLJC/Kxg7diz5+PiQi76+wtDPWs4A1MTKqkTrKw9Y8Jegwga/trbi4J8yfjwtLWDnowD1
6tSpxJ+LRCKh7du3k6OjI61atUrh9dexY8dS/fq21KBBO7K0bEx6elWpXz/PHGEUFxdHvr6+9PPP
P1N8fHyJ160MiURCnz9/JstKlehNAd93Dz6ftm/fru6SSSaT0eLFi+mXX35R6WUyqVRKPXv2pNev
Xyu1n0gkotmzZ5OHh0epveORyWT0/PlzGj58OA3X1s735/YYoIb5nJBoCna/ewmTSlMASAHk1VUy
FVKpGP369UPnzp3h6uqKFi1aKNW74dGjR/D09ESNGjVQvXp11KhRQ75Ur14dfD6/2M9DW1sbXl5e
GDJkCPbv3w83Nze4ublh9OjR4PP5eP78OXbvPoz4+EkA/t+18+TJIHTt2htnzx5FaGgogoOD8eef
f5baPAJpaWmIiYlBTEwMvnz5kuPfmJgYJCUlybfV1tZGlSpVIBKJCmyXy+Wq/UYyqVSK8ePHw9LS
EkFBQSqth8vlYvXq1Rg3bhyOHTtW6O6kurq6mD9/Pm7duoVBgwZh3Lhx6Nevn8rqUoTD4cDa2hrt
27fHnf37gfT0Ej1eRcCCvwQ1btwYzZpZ4e7dYUhL247c4Z8KPt8FffsOxV9/BePq1avYs2cPpk2b
BisrK3yNjoZpAceQAGjSuDGCgoLw6dMn+RIeHi7/f9asT0DGWD7ZXxiyv0AUZgwWLS0teHh4wN3d
HQcPHkSvXr1ga2uLLVv2ICHhDwA5bwBKS2uDO3e8ULu2DX7+eViRJ+fOQkRITExUGOJZ/88e3Pr6
+qhWrRqqVauGqlWrolq1amjQoIH8MSMjo1yBaX3iBF4IhfgujxrSAbwmUjiVY2kRCAQYPnw4evfu
DU9PzxI5Rr169eDs7Ix169Zh7NixSu3bunVrnDhxAvPmzcORI0cQGBhYKjfg5Z5DTbn1moL14y9h
AoEAXbv2xt27Ft+Ef0bo9+lTF7t2bc51RvXmzRsEBARg5/r1OCeVorWCtt8BcOTzMWP5coz6+WcF
W+RERIiLi5O/IHz+/DnHi4VYLAYRgcPhwNzcXOGLg4WFRY77DmQyGRo1aovISHcAU/M4shS6ur2w
aFEXTJ48OfdaqRSxsbF5npV//foV0syZsTgcDkxMTOQhnvVv1v+rVq1a7BuDTp48iWH9++OYUIj2
36xLB+DB4yGlbVscOnVKLXPoxsbGwtPTE1OnTkWXLooGKlAdmUyG3r17Y9WqVflOYZmfa9euYebM
mZg0aRLc3NxUXOH/3b9/H93s7fMcviEVgAufjxZDhmDVxo0lVkd5wIK/FAgEAnTr1ge3bt0Ah5Px
JksmE2HAgEEKQz+7Y8eOYdRPPyFUKMwR/u8AOPJ4GD9/PsYrCNPikMlkiI2NVfji8PnzZ/kNTVwu
F9WqVcPx45fx5ctGAJ3zaXUWuna9gSZNmiAmJgaJiYngcDggImhpaaFKlSo5gjx7oJuZmZX6Hc5Z
4b9bKIR15mMEYJqaQ//169cYOXIkVq5cWewbyZQ55rhx43D8+PEij+8kFAoxZ84cxMXFISAgQOG0
oqpw6dIlDHBxyRX+WaFft08fbN61q8TmNS431PfxgmaRSqUUGxsrX75+/Vro3ixHjx6lKnw+2ZuY
kL2JCbU3NCQzbW1qbGNDgwYNoq1bt9Lnz59L+BnkJhKJKCIigmrUaETAxQI+xJ5JPj4+FBkZSQkJ
CWWuJ48iJ06coHoWFmRlZiZfBrm65tmzqaTdvHmTHB0d6d27d6V+7LVr19KqVauK3c6VK1fIwcGB
Tpw4oYKqFAsLCyNzAwNyNjGhHpmLjYEBjRg8uNBdVCs6dsZfTrx8+RLR0dHyr01MTNC0aVN8/foV
p06dwsmTJxEbG4v27dvD1dUVtra2KjuriY2NxfPnzxEZGYnIyEi8ePECaWlp4HK5sLKywuHDF/Dp
0zrkf8Y/E7Vr70bHjh1hZ2eHDh06oGnTpmw8/UI6ceIE1q5di127dsHUtKBPflRPJpOhT58+CAgI
gLW1dcE75CM1NRUzZ86EUCjE8uXLYWxsrKIq/+/ly5d48eKF/Gs9PT04ODiwM/1MLPgrkPT0dFy7
dg2hoaG4ffs2LC0t4eLigu7duxf4x5WWloaXL1/mCPgvX76Aw+HAzMwM9evXR4MGDdCgQQPUq1cv
R08hL68xOHgwBkLhfgCKxh2Kgp5eJ3TqZA2JRAJra2vweDy8epUxQmSLFi3k47Vo0gichbVlyxZc
uHABW7ZsKbVJUBR5+/Ytfv75Z4SEhKjk0ltYWBjmzZuHWbNmoWvXriqokCksFvwV2Pv373HixAmc
PXsWYrEYnTt3hq2tLdLT0/HixQtERkbizZs3SE9Ph76+PurVq5cj4M3NzQvVRVAsFsPOrgvu3TOC
THYEOcM/I/T//HMc/PwmQSQSITQ0FHv37gURoX///qhduzZu376Na9euIS4uDjVq1ECHDh3QoUMH
2NjYaOxZGhHhjz/+QHJyMpYtW1Ymvg8bNmyAQCDAxIkTVdJeSkoKpk+fDplMhqVLl8LQ0FAl7TL5
Y8Ffgs6dO4fgZcuQfb7Pn3x8MGDQoBI9blJSkvys/fnz53j+/DkSEhIQFxeH1NRU+QxK/fr1w6BB
g4o9SfmVK1ewcOFCpKVxcf26EGlpzQFwoKXFha7uYVha6uPw4b/RqFGjHPvFxsZi//79OH78OGrX
rg0vLy/Y29vj06dPiIiIQHh4OJ4+fQpdXV20bt0adnZ2aNeuHYyMjIpVb3kgkUjwyy+/oHHjxpgw
YYK6y5EjIvTt2xdLly5V6ZSa586dw8KFC/H777/DwcFBZe0yirHgLyGnTp2CV//+WCwQZEz2DCAN
gB+Ph2UbNmDI0KHFal8ikeDNmzc5Av7jx48AAGNj4xxn7tbW1jku9RARnj59itDQUISFhYHH46F7
9+5wcXEpcCanLK9evYKvhwdio6MRGxuLGjVqoK6NDdo4OGDz5s2oXr06WrRogU6dOqF9+/YYPHgw
jhw5AhMTE4XtRUZGYufOnYiIiMAPP/yAoUOHol69ehnft7Q03L59Wz77VHJyMr7//nt06NABdnZ2
qFu3rtpvplKllJQUDB06FEOGDMGAAQPUXU4u79+/h6+vL0JDQ1Xa2yopKQlTp06Fnp4eFi9eXOwT
EiZvLPhLQFboHxEI8O30JI8BdCtk+BMRYmJiclx3f/XqFcRiMbS1tVGnTp0cAV+jRo0iBWBCQgLO
nDmD0NBQREdHo02bNnB1dUXbtm0V/mG/evUKju3a4be4OHTM9uuzXl8fz+rVg22nTrC2tkbjxo3R
rVs3AEBERAQCAgKwf//+fC9ZyGQyXL58GTt37sTHjx/Rp08fDBo0KMe1fyLC27dvER4ejvDwcLx6
9QoGBgZo27YtOnTogNatW6t1HP/iiI6OxtChQzF37lx07NhR3eXkafPmzUhISMCUKVNU3vbp06fh
7++P+fPnl9od3pqGBb+KCQQCWFSujFMiUa7Qz/IEwA/6+rj//Dlq1aoFgUAgvySTFfDx8fEAIL/T
NCvg69atW6If8EmlUty8eROhoaG4ceMGqlWrBhcXFzg7O8PU1FQe+jPj4zFGJsuxrwzACB0d3K5Z
E5PnzoWOjk6Ou0qDg4Px5csXzJ07t1C1CAQCHDt2DAcOHICOjg48PDzQs2dPhRPXpKSk4MaNG4iI
iMDNmzeRlpYGGxsb+bsCdU4IXliRkZEYM2YM1q1bh4YNG6q7nHwREfr164fFixeXSK0JCQmYPHky
TExMsHDhwnL7Ql5WseBXsbi4ONSrUQNxBYz3UldHB5Z2djA0NASfz4e1tXWOgC8rvVs+ffqEEydO
4PTp0xAIBPjw7BkGv3mD6Xn82sgA9NXRQbVhw2BjY5PjTl0igq+vL/r27QtXV1el6oiOjsbevXtx
8uRJ1K9fH15eXmjTpk2e73BEIhG8+vfH9fBwiMViSNPToaWtjb5eXhg+fDhatGhRqJnPFDl58iQW
+vlBJv3/AACuAwdi5rx5Rb7kFB4ejt9//x3bt29HjRo1itRGaYuKioKPjw9CQ0NLrFtuSEgIVqxY
gcWLF6N9+4z7qIVCIX728sLzx4/l2/GNjLB+165idzXVGKV3y4Bm+Pr1K5nq6eU/HCdANoaGdP/+
fXWXq5S0tDRqbmVFZwt4bvMAGjNmDE2dOjVXG0KhkLp160bPnz8vch0PHjygqVOnkpOTEy1YsCDX
pCFisZgGurmRC59PDwF6lLkcAaiynh55enrKx8738/OjI0eOFHoc+ZCQEDLn8egfgK5mLmEANePz
afqkSUW6Me3QoUPUp08fSkxMVHpfddu6dSv5+/uX6DG+fv1Kw4YNIz8/P4qLi6PuP/xAP/F48u//
VYACOByyrFy5WL9XmoQFv4oVNvgbGRvTo0eP1F2uUp4/f06WhoaFCv4pkyeTl5eXwnbev39PTk5O
CoeiVkZ6ejqdOXOGvLy8yNXVlbZs2UKxsbHy0BcqqC0M/59BKz09ne7du0fr1q2joUOHkrOzM3l6
etK6devo3r17uYY5zgr9awra/a+I4b9mzRoaMWKEUlNdliUymYz69etXKr/L+/bto+omJuSup6dw
kpzNLPwLjQW/igkEAjIzNKRj+QTjZYAq8/lFnqtUHV6/fk0ODg7UsWnTQgX/nNmzydXVNc/2Lly4
QB4eHiobuiE5OZm2b99OrVu3piba2gpDP2s5CVCdatUUthMdHU1HjhwhPz8/6tmzJ7m5udGcOXPo
xIkTZKinRxH5tPsfQLX5fLp+/XqB9UqlUvLz86NZs2aVi+Er8vPhwwf64YcfqFndumRuaChfGlha
qvQFITAwkJzzCP2sZQWHQ93t7FR2zIqKBX8JuHHjBlXNI/wvZ55xnj59Wt1lFtq7d+/IwcGB3r59
S2O9vcmNz6e0PP7wPgBUj8+nvXv3kouLS77tBgQE0NKlS1Va6549e2iQgUG+L0xRANWsVKlQ7YlE
Irp+/ToFBgYSB6D0Al70OpuYFDgPclpaGg0dOpSCg4NV8IzV782bN2RhbEwrOByKAeTLXxwOVa9U
SWXhv3DhQprB5eb7/b8E0A9NmqjkeBUZC/4SkhX+fwC0MnPxL4eh/+HDB+rcuTO9evWKiDKun//Y
o4fC8P8AUB09PfKfP5+IqMDgl8lkNHTo0DwnLi+KPXv20E9GRioL/uy4HE6xgz8hIYHc3Nzo2LFj
xXiWZcfbt2/pu6pVaVUegbwrM/wfP35c7GOx4FcdNkJWCWnTpg1OXbqEvzZswFeijAc5HBz08ECn
Tp3UW1whRUdHw9PTE5s2bUKdOnUAADo6Oth37Bh+6tMH3S9eRJvMIZoBYD8RRk6ZgmmzZwPIGDtf
JpPl2W+fw+EgODgYvXv3Rr169WBlZaWSuqmY60vKhw8fMHz4cCxatAht27ZVUxWqFbhkCfrHxuK3
b7r2ZhlChA+JiVg4cyZ2HzlSytUxeWHBX4JatmyJlsHB6i6jSL58+QIPDw+sW7cuVxc5HR0d7Dt6
FFu2bEFKSor88Sq7d2PeggXyrytXroy4uDhUqVIlz+Pw+Xxs3LgRPj4+OHbsWLH7azds2BDjpVJc
A3JNogJkdDedp6+PFkUYy97GygrLP3zAtDym9gsD8FgiUXjPwKNHjzBu3Dhs2rRJfkdyRZAuEqFe
HqGf5Tsi3CnEdJYFadCgAfz09fGzQABFd2VIAKzi8WDTrFmxj1XhqfstB1P2xMbGkpOTEz18+LDQ
+yQnJ1P//v1zPDZlypRCX989efIkjRgxQiUfdIaGhpI5j5frg1gpQN76+tSxVasi9Sj68OEDWdes
Sf4KJvS+CFCVzN5C3/r333+pe/fuhe4yWp786u1Nawq4/LUPoEE9eqjkeMv9/akun0/vvzmGGKD+
PB65OjpSWlqaSo5VkbEzfiaH+Ph4/PTTT1ixYgWaNGlS6P0ePnyIZt+caVWrVg0xMTFo3Lhxgfv3
6NEDt2/fxrp16/Drr78qXXd2Li4u+OvgQfQeOBD9iJB1S9VrAGkNG+JEWFiRRoGsWbMmLly/Dsd2
7fDkyxdYZJ7ppgPYoaeHfceO5ZoKcd++fTh48CAOHTpUYceeKc1La5OnTQMAOPz5JwZkvouQSqW4
p68P/fbt8U8x53TWFCz4GbnExES4u7tj8eLFaNGihVL73rt3L9c+1apVw5cvXwrdxowZMzB48GA0
b9682GO0uLi4IOTCBdy5c0f+WBsdHbi7uxdr6N+aNWsi7OZN7Nq1C0KhEFFRUQCAeS1agMPhIDEx
ESYmJiAirFixAq9evcK+ffsq7IQzP3Tpgun79sFVIEAdBeujAfzB5+PX7t1VdszJ06bhe2tr+UQr
V65cgbWlJVauXMlCv7DU/ZaDKRuSkpLI2dmZIiIiirS/r69vrikBT58+TStXrlSqncTERHJ0dKSP
Hz8WqY7SEh8fT60bNqTWRkbkaGJCjiYm1M7IiJrWqUOfP3+m3377jRYsWFDu++gXxtrVq8mKz6dX
31x++QyQDZ9Pf8yeXaLHv3v3Lk2bNq1Ej1HRsOBnKCUlhVxcXOjSpUtFbqNHjx65Qu7evXs0Y8YM
pdt6+vQpOTs7k0gkKnI9JSkr9Cfo6pIsW9DJAJqpo0NVDQxo9erV6i6zVK1dvZpq8vn0o7GxfPmu
FEKfKONmuJ49e5b4cSqSivn+kyk0oVCIwYMHY8qUKUUeBjg9PR1aWlq5BijLusavLBsbG4wZMwYT
JkzAunXrilRTSZFIJOhub48fXr1CgFiM7M+YA2CBRAIiwqaVK+Hj46Mxo0r+Mm4cWtja4vPnz/LH
xlauDEdHxxI/NpfLBZ/PR3JyskZM0qMKLPg1mEgkgoeHB8aOHVusP9AXL14onI2pSpUqiI2NLVKb
ffv2xa1bt7B161Z4e3sXuTZVi42NxdvXr3H9m9DPwgGwMD0de2Ji8PHjxwrVdbMgHTrkNRB5ybO3
t8fVq1fRo0cPtdVQnqh/Ek9GLcRiMYYMGQIfHx90L+YHb4o+2AUAbW1tSLMNXaysP/74A8ePH8fN
mzeLU57KaXE4CkM/CweAdgWaEaw8cHBwwMWLF9VdRrnBgl8DSSQSeHl5YejQoUqPi6/I3bt3le4F
VBhaWlrYunUr/Pz8lOodxGieZs2a4cGDB+ouo9xgwa9hHj16hEqVauLo0dPw9PSBkZE56tRpilev
XhW5zadPn8LGxibP9URF78ltamqKVatWwdvbG+l53DFbmrhcLgRSKRLz2SYVQHJ6er5TTDKqpaWl
BR6Pl+NOciZv7Bp/BXTq1CmsX7Iko69JJo/Ro9GkWTPY2naEWLwMQB/5OoHgb7Rv74Rr1/5F3bp1
lToWESE9PR06OjoK15uYmCAxMRGVKlUq0nMBMs7mPD094efnBxtra+zM/oEvh4OxM2bAffDgIrev
jKpVq8LLyws99uzBKYEA304dnwrAlc+Ha+/e+P7770ulJiZD1nV+Z2dndZdS9qm5VxGjYsePHydz
Ho+2I2PGqSOZt8xX19cnbS0eAdsU3lnP5QZTlSq15aNwFtbHjx/J29s7z/UTJ06kZ8+eFfdpERGR
U+fOVEtXl05njsJ4CaDjAFXn8WjXjh0qOUZhyGQy+nXkSGrH59PXzOECxAAlANSZz6cRP/1EUqm0
1OphMty+fZumT5+u7jLKBfZetAIJCQmB96BBCBEK4YWMc/o+ANwB/JuWBiOpJM99ZbLR+Pp1CBYs
WK7UMfP6YDdLUbt0fmvNypV4feMGLonF6A6gY+biBuCsUIipo0dj986dxT5OYXA4HKzZtAnthw5F
NS4X/MylCpeL+j/+iM27d7PLPGrQvHlz3L9/X91llAvst7OCSE1NxeABAxAiFELRgL82AMKRDn2M
ARClsA2i7yAWK3cd/d69e2jZsmWe66tWrVrs4H/37h1+nz4dF4RCfKdgfWNkhL/vyJFISkoq1rEK
i8PhYGVwMCRSaY5l486dLPTVhF3nLzz2G1pBpKWlQRdQGPpZbACYQRdAssqOe//+/VyDs2WnijN+
gUCAarq6CkM/S2MAPC0tiMXiYh2LKd/s7e0RHh6u7jLKPBb8TDb5j6uuSHJyMoyNjfNcr6pLPQxT
GKw/f+GwXj0aJ6+ule/A5y9Ft25/5rt3SkoKlvn7IzUpCWKxGG9fvMCG9evhO2ZMriEbABb8TOlq
3rw5ZmfOAMfkjQV/BcHn86Glq4sjIhH65rFNGICvSEXGXEXZvQOf74gFCyZi2DDPPI+RkpKCnp06
ofrjx2ibeUnFG8D6KVPw5sULLF6xIlf4V61atdg3X1WtWhVfARwH0CuPbXZwONDj84s15DJT/mlp
aUFfXx+pqakVdv4DVWDBX0HweDycungRPR0cgOTkXOEfBmAAn4/B7h7Yv78PtLVt5etSUy9jypRx
mDhxXJ7tZ4W+zZMn2CAW57hGOEIgQJcNGwAgV/jr6upCIsm7N1FhmJmZIfT8ebg5OWFzSkqu8N/B
4WBGpUo4f/Uq9PX1i3Uspvxr3Lgx/vnnH/mcDubm5mzwtm+w4K9AWrVqhZOZ4X8nOVl+c1EagJV8
PvYfPw4nJycMGxaWY/C0uLgeuHv3br5tjxk6FNZPnmCDSJTrgyEzAOcFAjhu2IBGLVrAy8tLlU8L
QMbk9SH//gs3JycMEQjAy7w5LZHDwWETE5wPD8/37mFGM8ybtxBLlqwGYAQ9PV0QEfT10xER8W+u
uaM1GQv+CqZVq1Y4cvo0Rnt7w9jICG3atAGXy8WRn36Cvb09AKBz58659hs4cCDevn2L7777TmG7
Ua9f408FoZ/FDEBvoRDv379XzRNRoE2bNjh79SqOHz8uf4wP4OKgQeyPmsG8eQuxbNlOSCTPAFRH
1htNgWAz7OycWPhnw4K/grl79y5mzZqF1evXw8HBodD7zZ49GwsXLsSmTZtUXpOhoSFSUlJUcv29
WbNm+XYfZTTTokXLsGzZTggEFwBUz7GOyAdxcYCdnRNu374CKysr9RRZhrDunBUEEWHNmjVYsGAB
9u/fr1ToAxm9IVJSUvDy5UuV18Z69jAlbe3arRAIduHb0M9C5AOBoBNOnz5duoWVUSz4K4C4uDi4
u7tDIpHg77//hrm5eZHamTNnDubPn69wnYmZGc5raeW5bxqAK/r6uQZje//+PbhcLm7cuIFnz57h
69evRaqNYQpWUC8e1ssnCwv+cu7KlSvo378/pk6dikmTJhVruIBGjRoBAJ48eZJrXfCuXdhnYQF/
7dxXB9MA/Mjno2qXLhgzZoz88bWrV6N5/fo4vmED5owcib5t26Lh99/j1q1bRa6RYZjiY9f4yymp
VIrFixcjMjISR48ezffuWWXMnj0bv//+O/bs2ZPj8Ro1auDijRtwaNsWidHRaJ9tZq1gPh9GTk7Y
c/gwtDNfGNauXo1lM2bgjkiE7IMTHwfg6uiI0AsX0Lp1a5XUzDAZPYgLGopEdUOVlHfsjL8c+vz5
M/r27Yvq1atjx44dKgt9ALC2tgafz1c4ymFW+L9zdcXWzp3lS+MRI3KE/uYNG7BsxgxcEAjw7Yj0
vQBsTkmBq6MjmzGJUZmJE8eAz/dAXgMQcrlrYWgYgZ49e5ZuYWUUh6gY0yMxKiWVSrFg7ly8ynap
xdDUFPOXLYOZmRmAjElWli1bhjVr1sgvzajamzdvMG3aNBw4cKBI+3du3hwzHjxAftNeT+ZwYPrn
n+z2ekZl/P2XY/784MyePbXkj3O5a2FmtgzXrv2LOnXqqK/AMoRd6ikjpFIpRnp44F1ICEYIBPLH
w3V00O3qVZwIC0NAQABSUlIQEhICHo9XYrV8//33MDMzw61bt4p8Oaag6kquekZTTZ8+BQAwd24j
6OhkvQsmGBrqIiKChX52LPjLgKzQfx8SghCBIEffg6ESCfzevEGzunWxJCgII0aMKJWaZs2ahXHj
xuHw4cOlcjyGUYXp06dg5MhhOYbnrly5comeKJVHLPjLgODgYLw4fhxnhMJcHc44AJZKJBADOHXw
YKkFv6WlJWrXro3w8HB06NBBuZ05HBQ0HUoSh4OijKrz33//Yf26dZBk+8Nu2749evXKa/g2RtMU
tTuzJmHBXwbExsaiq4LQz8IB0EciwYLPn0uzLMyYMQOjRo3KMURCYfwybRpGjxyJOkIhGitYv4vD
wT/GxrgwaJBS7f7333/o0r49Wr5/j3rpGTOFEYCfeTzErlmDESNHKtUew2gqFvxMniwsLGBjY4OL
Fy8qdSew++DBSE9PR7fRo3H2m/DfxeFgmokJzl69ivr16xe6zazQ7x0Vhfnp6cg++LO7UIgu4zJG
FmXhzzAFY8HP5MvPzw/Dhg1D586dFU60kpchQ4cCANr5+ICX7aYyHR4P565cUbpH0oAePeAWFYX5
Egm+raIBgPNCIRx/+w31bWzkg9ExDKMY68dfBlSrVg2n+Pw8by8hAAd1dWFRq1YeW5Qcc3NztGrV
Ck4zGwUAAAoJSURBVGfPnlV63yFDh+LTf//hyfv38uX1p09F6ob6+s0b/Kwg9LM0AODA5eLdu3dK
t80wmoYFfxng6+uLFgMGwEVB+BOACbq6uG1tjXXbt6ujPEyePBkrVqxAUW75MDY2hrm5uXxhE6Uw
jPqx4C8DuFwu1m/bhkYDBqAnn49NgHzx1tXFNWtrnL5yJdcAaKXF1NQU9vb2CAkJUcvxGYZRLXaN
v4zICv9l1ta4ke3O3UqVKuH0okVqC/0sEyZMwI8//ghXV9diDQRXVEZGRrgcHw+PPNYnArgnlWIw
m2KPYQrEgr8M4XK5mFZGhzAwNjZG165dcfjwYfTv37/Uj7/7yBH0dHCAXlISvj16IoBuPB4kVarg
+fPnSE9Pl48bxDBMbuxSD1No48aNw7p16yDNNjJnaWnZsiVOXryIX42NsQ7AmczlNABnPh9tPDwQ
+fYtTE1N4eLignv37pV6jQxTXrBB2hilBAYGolq1avDwyOuiS8m6e/cuZo8fD0lamvwxO0dHzPP3
l3c3jY6OxpQpU1CzZk38/vvv4PP5aqmVYcoqFvyMUoRCIVxcXHD27Nkyfznl+PHjCAgIwOzZs9Gl
Sxd1l6NWd+/eRVLS/wfSqF69ulI30DEVCwt+Rmlr166FgYEBhg8fru5SCpSUlIRZs2ZBKBRi6dKl
qFy5srpLKnXL/f0R8OefsNbVlT/2RCzGln370Lt3bzVWxqgLC35GaSKRCD169MCZM2ego6Oj7nIK
JSIiArNnz8aoUaPg7u6u1F3I5dlyf39smD8fFwQCWGZ7/BYAVx4Pm1j4ayQW/EyRbNq0CVKpFIMH
D5Y/xuVyYVSGu1OKxWL4+/vj/v37CAwMRO3atdVdUokKDgrCimnTcoV+lqzw3xsSAicnp9Iuj1Ej
FvxMkXz9+hWNrayQKhaDm3n2LJbJMOG337Bo+fIyfUb99OlTTJ48GT179sQvv/wCLS0tdZdUItw6
doTPlSvom882CwEkTZqEJStWlFZZTBnAunMySktKSkIvJyf0EYmQKJEgUSxGoliMD+npOBkcjBmT
JxdpeIfS0rBhQ4SEhEBHRweurq549OiRuksqMQV9/F62P55nSgoLfkYpqamp6NGxI1pERmJ9enqO
XyAzAOcFApzasAGzpk5VV4mFwuVyMWbMGGzZsgXz58/HnDlzkJatiyjDVGQs+BmlXLt2DeLXrxEk
Ein85TEDcEogQMCqVaVdmtLWr9+I1q0dERZ2B2vWbIexcU24u3uV6XcrykhJTUVMAdvEcDhqGYKD
US/2E2eUQkSopKWV7y+OaeZ2ZVlQ0HpMnrwQ0dE7ERNzAomJ5yGRXMKhQ3fRpIkt4uPj1V1ikRAR
Tpw4AVdXV1SztsY0Hg//5rHtJi4XBytXhs+YMaVaI6N+7BIfUyJkMlmueXANDQ1hampa4GJkZFSi
Hw6vXRsMPz9/CIUXANTJsS49/RJev3ZC06a2WLVqmVrGJSqK9PR07N+/H9u2bYODgwN27tyJypUr
IywsDANcXLBfIIBDtu23cLmYb2qKf69dQ926ddVVNqMmrFcPo5Rz585hXv/+uJKU93TqiQCqamlB
lDkvLpBxJpqSkoL4+PgCl+TknLMSEJFSLxr5XbpIS0uDkVElpKc/wbeh/3/x4PGaYOhQNyQkJCAw
MBA1atRQ4rtUegQCAbZs2SIfPG/EiBG5hqgICwtDHxcXJAmF8sesqlbF2StXUK9evdIumSkD2Bk/
o5RWrVrhP2NjLBYIMCNbsGcRAhjA52Owm1uOxzkcDoyMjGBkZKR0/3kiQmpqao4Xh7i4OMTHx+Pt
27e5XjS+PZcxMDCQvzAYGBhAJuMg79AHAFPo6FTD6NGjoaOjA29vb/Tt2xe+vr5l5np4XFwc1q5d
i7CwMHh7e+PMmTN5DqHRuXNnJKSmlnKFTFnGzvgZpX369L927iak7TuO4/jnb6LV4GJ3cAprKRY7
fGDUBVYVxoxeKp2b0oPsODwqExTR2w6iNx9O8eA2Zy+2epIhCB3iEPSwi4xSKfUgaFGZpaP4GOK/
2aGzq0uqTKJmft+vW8zT75C8Az9//++qKktL9c36+qH470r6yufTB7dv697YWFLM8vn3j8bq6qpq
au7KdXeOfJ7fH9D09A8KBAJyXVcDAwOanJxUX1+fCgoKzmj1sVZWVtTX16fFxUU1NTWpuro6qa+Z
QHIi/DiRg/h7X76U5+/w/BmJ6PPq6qSJfjzb29u6fDlb+/vHhf8TTU//qEAg8OZvy8vLamlpUUlJ
iTo6OpT21uyb07awsKCenh5tbW2ptbVVZWVlZ/beuHgIP05sc3NTS0tLb26npKSoqKgoabZD4nFd
Vzdu3NSzZ/WKRL6L+xjHGVFWVpuePv1d2dnZh+6LRqMaGxvT4OCgurq6VF5efqrrnZubU39/v/x+
v9ra2lRYWHiq7wcbCD/MWV9fV2lpldbWvo6Jv+OMyO9v0+zsLyouLn7na7x48ULt7e3y+Xzq7u5O
6IyigyOZoVBIhYWFamlp0ZUr8abtACdD+GHSQfyfP/9IjvN6VHM0GlZq6vSx0X/b1NSUurq61Nra
GnN8NRwOx4yDKCoqUkZGRtzXikQiGh0d1fDwsILBoBobG02OkcbpI/wwa2NjQxMTE4dOAVVUVPzn
c+07Ozvq7OzUysqKent7lZubq62tLQWDX+jJk3V5vZmSJNfd1bVr72l29qGysrIOPf+4I5lAIhF+
IEHm5+fV0dGhuro6DQ2N6vHjfO3tfa9/LpCP6tKlZuXn/6bZ2Yfa399XKBTSzMyMGhoaVF9fn7T/
FMfFQviBBAqHw8rPv6nV1U/16tU9xU5FiSot7VtlZv6sW7eK1dzczJFMnDnCDyTQ2tqarl//WHt7
f+jdo7CiSk+/qkePfuXKWZyL5D13B/xPOU6qjv5qOfJ6089qOUAMwg8AxhB+IIEcx5Hr7ko66srg
sFx3m319nBvCDyRQTk6Oamtr5fN9qfjxD8vnu6vKys+Ul5d31ssDJBF+IKEcx9H9+0O6c+fDOPF/
Hf1g0Kfx8ZGkHm2Bi41PHpBgHo9HDx78pJqaq/J43pfX65PX65PH41dVVabGx0eUmpp63suEYRzn
BE7Rzs7h7Z6MjAz29nHuCD8AGMNWDwAYQ/gBwBjCDwDGEH4AMIbwA4AxhB8AjCH8AGAM4QcAYwg/
ABhD+AHAGMIPAMYQfgAwhvADgDGEHwCMIfwAYAzhBwBjCD8AGEP4AcAYwg8AxhB+ADCG8AOAMYQf
AIwh/ABgDOEHAGMIPwAYQ/gBwBjCDwDGEH4AMIbwA4AxhB8AjCH8AGAM4QcAYwg/ABhD+AHAGMIP
AMYQfgAwhvADgDGEHwCMIfwAYAzhBwBjCD8AGEP4AcAYwg8AxhB+ADCG8AOAMYQfAIwh/ABgDOEH
AGMIPwAYQ/gBwJi/AESrG07cByZjAAAAAElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="{{ site.baseurl }}/docs/visual#quickVisual"><code>quickVisual()</code></a> makes a graph with the different types of nodes coloured differently and a couple other small visual tweaks from <em>networkx</em>'s <code>draw_spring</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Making-a-multi-mode-network">Making a multi-mode network<a class="anchor-link" href="#Making-a-multi-mode-network">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>For any number of tags the <a href="{{ site.baseurl }}/docs/RecordCollection#nModeNetwork"><code>nModeNetwork()</code></a> function will do the same thing as the <code>oneModeNetwork()</code> but with any number of tags and it will keep track of their types. So to look at the co-occurence of titles <code>'TI'</code>, WOS number <code>'UT'</code> and authors <code>'AU'</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[40]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">tags</span> <span class="o">=</span> <span class="p">[</span><span class="s">&#39;TI&#39;</span><span class="p">,</span> <span class="s">&#39;UT&#39;</span><span class="p">,</span> <span class="s">&#39;AU&#39;</span><span class="p">]</span>
<span class="n">multiModeNet</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">nModeNetwork</span><span class="p">(</span><span class="n">tags</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">multiModeNet</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[40]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 108 nodes, 163 edges, 0 isolates, 0 self loops, a density of 0.0282105 and a transitivity of 0.443946&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[41]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mkv</span><span class="o">.</span><span class="n">quickVisual</span><span class="p">(</span><span class="n">multiModeNet</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Beware this can very easily produce hairballs</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[42]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">tags</span> <span class="o">=</span> <span class="n">mkt</span><span class="o">.</span><span class="n">tagsAndNameSet</span> <span class="c">#All the tags, twice</span>
<span class="n">sillyMultiModeNet</span> <span class="o">=</span> <span class="n">RC</span><span class="o">.</span><span class="n">nModeNetwork</span><span class="p">(</span><span class="n">tags</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">sillyMultiModeNet</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[42]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 1184 nodes, 59573 edges, 0 isolates, 1184 self loops, a density of 0.0850635 and a transitivity of 0.492152&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[43]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mkv</span><span class="o">.</span><span class="n">quickVisual</span><span class="p">(</span><span class="n">sillyMultiModeNet</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
liDDN88hw0gG8o3iXWpWEf0XsOHxtMLtdmMYPvr06a6hr5pMg1+p81BWVsbQoXeRl7eJQMCBabYG
emO3HyEQOIes/AkP/3JgGLIXoBdST+cYcBQYhwwZBXC7P6Fnz3P07du9uoGKYRj069ePm266qfrZ
MjMzcblc38AnVS2JBr9S58k0TUpLSzFNk/fff5+ioiLi4uJYvnwFK1fmEQjcWX1fu/1Drr++LQ89
9CBjx06irOwJZLJ4N/Albvc2xo0bS2ZmJhMmTCAhIeHb+liqBdPgV+prtGLFCg4ePFj9c6tWrcjJ
ycHlcpGbm8vrr79N6C/QbrcxZcoEXXuvvnYa/EopZTG6jl8ppSxGg18ppSxGg18ppSxGg18ppSxG
g18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18p
pSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxG
g18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18p
pSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSxGg18ppSzm
/wGPnBn0EphgMQAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Post-processing-graphs">Post processing graphs<a class="anchor-link" href="#Post-processing-graphs">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>If you wish to apply a well known algorithm or process to a graph <a href="https://networkx.github.io/documentation/networkx-1.9.1/"><em>networkx</em></a> is a good place to look as they do a good job at implementing  them.</p>
<p>One of the features it lacks though is pruning of graphs, <em>metaknowledge</em> has these capabilities. To remove edges outside of some weight range, use <a href="{{ site.baseurl }}/documentation/metaknowledgeFull.html#dropEdges"><code>drop_edges()</code></a>. The functions all mutate the given graph, so if you wish to keep the original keep a copy. For example if you wish to remove the self loops, edges with weight less than 2 and weight higher than 10 from <code>coCiteJournals</code>.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[44]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">minWeight</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">maxWeight</span> <span class="o">=</span> <span class="mi">10</span>
<span class="n">proccessedCoCiteJournals</span> <span class="o">=</span> <span class="n">coCiteJournals</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">mk</span><span class="o">.</span><span class="n">dropEdges</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">,</span> <span class="n">minWeight</span><span class="p">,</span> <span class="n">maxWeight</span><span class="p">,</span> <span class="n">dropSelfLoops</span> <span class="o">=</span> <span class="k">True</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[44]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 90 nodes, 471 edges, 1 isolates, 0 self loops, a density of 0.117603 and a transitivity of 0.211703&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Then to remove all the isolates, i.e. nodes with degree less than 1, use <a href="{{ site.baseurl }}/documentation/metaknowledgeFull.html#dropNodesByDegree"><code>drop_nodesByDegree()</code></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[45]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mk</span><span class="o">.</span><span class="n">dropNodesByDegree</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[45]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 89 nodes, 471 edges, 0 isolates, 0 self loops, a density of 0.120276 and a transitivity of 0.211703&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now before the processing the graph can be seen <a href="#Making-a-co-citation-network">here</a>. After the processing it looks like</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[46]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">nx</span><span class="o">.</span><span class="n">draw_spring</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
X8YYY8zM/h94BmararCoqgAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Hm, it looks a bit thinner. Using a visualizer will make the difference a bit more noticeable.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Exporting-graphs">Exporting graphs<a class="anchor-link" href="#Exporting-graphs">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Now you have a graph the last step is to write it to disk. <em>networkx</em> has a few ways of doing this, but they tend to be slow. <em>metaknowledge</em> can write an edge list and node attribute file that contain all the information of the graph. The function to do this is called <a href="{{ site.baseurl }}/documentation/metaknowledgeFull.html#writeGraph"><code>writeGraph()</code></a>. You give it the start of the file name and it makes two labeled files containing the graph.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[47]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span class="n">mk</span><span class="o">.</span><span class="n">writeGraph</span><span class="p">(</span><span class="n">proccessedCoCiteJournals</span><span class="p">,</span> <span class="s">&quot;FinalJournalCoCites&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>These files are simple CSVs an can be read easily by most systems. If you want to read them back into Python the <a href="{{ site.baseurl }}/documentation/metaknowledgeFull.html#readGraph"><code>readGraph()</code></a> function will do that.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[48]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre> <span class="n">FinalJournalCoCites</span> <span class="o">=</span> <span class="n">mk</span><span class="o">.</span><span class="n">readGraph</span><span class="p">(</span><span class="s">&quot;FinalJournalCoCites_edgeList.csv&quot;</span><span class="p">,</span> <span class="s">&quot;FinalJournalCoCites_nodeAttributes.csv&quot;</span><span class="p">)</span>
<span class="n">mk</span><span class="o">.</span><span class="n">graphStats</span><span class="p">(</span><span class="n">FinalJournalCoCites</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[48]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&apos;The graph has 89 nodes, 471 edges, 0 isolates, 0 self loops, a density of 0.120276 and a transitivity of 0.211703&apos;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>This is full example workflow for <em>metaknowledge</em>, the package is flexible and you hopefully will be able to customize it to do what you want (I assume you do not want the Records staring with 'A').</p>

</div>
</div>
</div>
{% include docsFooter.md %}