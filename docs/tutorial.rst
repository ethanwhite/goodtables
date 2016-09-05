Tutorials
=========

Some tutorials for using and extending Good Tables.

1. Implementing a custom processor
----------------------------------

# TODO: This is unfinished.

Implementing a custom processor that can be invoked in a pipeline is easy.

Let's write one that checks that values are in a certain range.

For data, see the file `custom-range.csv` in the `examples` directory.

In our data, we have name, age and city data for a group of people.

We want to ensure that all the people in our data are in the 25-50 age range.

For demonstration, we'll write a pretty specific processor for this.

Of course the implementation could be made more generic for a range scenarios.

Our processor class::

  class AgeRangeProcessor(object):
      column_name = 'age'
      column_type = int
      column_range = (25, 50)
      report = {}

      def run_row(self, index, headers, row):
          valid = True

          return valid

      def run():
          valids = []
          return valid, report

      def generate_report():
          return report

As you can see, we hard coded `column_name`, `column_type` and `column_range`.

Also, we are running our validation through the `run_row` method, which is the most common method used for validations.

However, we could easily run the same validation in the `run_column` instead::

    # stuff
    def run_column():
    valid = True
        return valid

So, let's see it in action. First, we'll run the processor in 'stand alone' via its run method::

  processor = AgeRangeProcessor()
  filepath = 'examples/custom-range.csv'
  valid, report = processor.run(filepath)

And the same, but part of a validation pipeline using the structure processor with our `AgeRangeProcessor`::

  processors = ('structure', 'my_module.AgeRangeProcessor')
  filepath = 'examples/custom-range.csv'
  validation_pipeline = ValidationPipeline(filepath, processors)
  valid, report = validation_pipeline.run()
